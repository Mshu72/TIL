###  **`org.springframework.util.StringUtils` について**

`org.springframework.util.StringUtils` は、**Spring Framework** が提供する文字列操作用のユーティリティクラスです。文字列の操作や判定を簡単かつ安全に行うための静的メソッドが多数用意されています。

---

###  **主な特徴**
- **`null` セーフ**: 多くのメソッドが `null` 値を安全に扱えるように設計されています。
- **日常的な文字列操作の簡素化**: 空文字判定、トリミング、分割、結合、パターン変換などをサポート。
- **Spring プロジェクト向け最適化**: Springベースのアプリケーションに特化した文字列操作が可能。

---

###  **よく使われるメソッド一覧**

| メソッド名                     | 説明                                      | 戻り値例                                |
|----------------------------|-----------------------------------------|--------------------------------------|
| `hasLength(String str)`   | 文字列が `null` でなく、長さが1以上か判定        | `"abc"` → `true`、`""` → `false`   |
| `hasText(String str)`     | 文字列が `null` でなく、空白以外の文字を含むか判定 | `"  "` → `false`、`"abc"` → `true` |
| `trimWhitespace(String str)` | 前後の空白をトリム（スペース、タブ、改行など） | `"  test  "` → `"test"`           |
| `capitalize(String str)`   | 最初の文字を大文字に変換                     | `"spring"` → `"Spring"`           |
| `uncapitalize(String str)` | 最初の文字を小文字に変換                     | `"Spring"` → `"spring"`           |
| `commaDelimitedListToStringArray(String str)` | カンマ区切りの文字列を配列に変換            | `"a,b,c"` → `["a", "b", "c"]`     |
| `collectionToDelimitedString(Collection<?> coll, String delim)` | コレクションを指定した区切り文字で結合    | `["a", "b"]` → `"a,b"`            |

---

###  **代表的なメソッドの解説と使用例**

#### 1️ **`hasLength(String str)`**
- **用途**: 文字列が `null` または空文字 (`""`) かどうか確認します。
- **ポイント**: `null` セーフで `NullPointerException` を回避できます。

```java
import org.springframework.util.StringUtils;

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.hasLength(null));  // false
        System.out.println(StringUtils.hasLength(""));    // false
        System.out.println(StringUtils.hasLength(" "));   // true
        System.out.println(StringUtils.hasLength("abc")); // true
    }
}
```

---

#### 2️ **`hasText(String str)`**
- **用途**: 文字列が `null`、空文字、または空白だけの文字列かを判定します。
- **`hasLength()` との違い**: 空白だけの文字列も `false` を返します。

```java
System.out.println(StringUtils.hasText("   "));  // false
System.out.println(StringUtils.hasText("abc"));  // true
```

---

#### 3️ **`trimWhitespace(String str)`**
- **用途**: 前後の空白文字を削除します。Javaの `String.trim()` よりも広範な空白文字をサポートします。

```java
System.out.println("[" + StringUtils.trimWhitespace(" \tHello World\n ") + "]");  
// 出力: [Hello World]
```

---

#### 4️ **`capitalize(String str)` と `uncapitalize(String str)`**
- **用途**: 文字列の先頭文字を大文字または小文字に変換します。

```java
System.out.println(StringUtils.capitalize("spring"));   // Spring
System.out.println(StringUtils.uncapitalize("Spring")); // spring
```

---

#### 5️ **`commaDelimitedListToStringArray(String str)`**
- **用途**: カンマ区切りの文字列を配列に変換します。

```java
String[] array = StringUtils.commaDelimitedListToStringArray("apple,banana,grape");
for (String s : array) {
    System.out.println(s);
}
// apple
// banana
// grape
```

---

#### 6️ **`collectionToDelimitedString(Collection<?> coll, String delim)`**
- **用途**: コレクション内の要素を指定した区切り文字で結合します。

```java
import java.util.Arrays;
import java.util.List;

List<String> list = Arrays.asList("apple", "banana", "grape");
String result = StringUtils.collectionToDelimitedString(list, ", ");
System.out.println(result); // apple, banana, grape
```

---

###  **`null` セーフな文字列操作の重要性**
多くの文字列操作メソッドが `null` セーフであるため、`NullPointerException` を心配せずに使用できます。たとえば、Java 標準の `String.isEmpty()` では `null` 値を渡すと例外が発生しますが、Spring の `StringUtils` はその心配が不要です。

---

###  **バージョン間の違い（Spring 5以降の変更点）**
Spring 5 以降では、一部のメソッドは `org.springframework.util.StringUtils` から `org.springframework.lang.StringUtils` へ移動しています。プロジェクトで利用している Spring のバージョンに応じて適切なパッケージを確認してください。

---

###  **まとめ：`org.springframework.util.StringUtils` を使うメリット**
-  **`null` セーフな実装**: `null` チェックの手間を削減  
-  **Spring プロジェクトとの統合性**: Spring 環境下での最適な動作  
-  **豊富なユーティリティメソッド**: 開発を迅速化する多様なメソッド  

Spring Framework を使用している場合は、文字列操作の多くをこのクラスで簡単に扱うことができます。
