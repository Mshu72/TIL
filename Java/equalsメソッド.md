Java 8 の `String` と `Optional` の `equals()` メソッドには、**共通点**もありますが、**根本的な目的と使い方が違う**

##  1. `String.equals()` の基本

###  主な用途：
2つの文字列が**内容として等しいかどうか**を比較する。

```java
String str1 = "hello";
String str2 = "hello";

System.out.println(str1.equals(str2)); // true
```

- これは **中身（文字列の内容）を比較**します。
- 大文字・小文字を区別します。
- `null` に対して呼び出すと **`NullPointerException`** が発生するので注意！

```java
String str1 = null;
str1.equals("hello"); // ❌ NullPointerException
```

---

##  2. `Optional.equals()` の基本（Java 8以降）

###  主な用途：
2つの `Optional` インスタンスが**同じ中身（value）を持っているか**を比較する。

```java
Optional<String> opt1 = Optional.of("hello");
Optional<String> opt2 = Optional.of("hello");

System.out.println(opt1.equals(opt2)); // true
```

- **中身の値が同じなら等しいと判定**。
- `Optional.empty()` 同士も等しいと見なされます。

```java
Optional<String> empty1 = Optional.empty();
Optional<String> empty2 = Optional.empty();

System.out.println(empty1.equals(empty2)); // true
```

---

##  大きな違い（ポイント）

| 項目 | `String.equals()` | `Optional.equals()` |
|------|------------------|--------------------|
| 比較対象 | 文字列の内容 | Optionalの中身の値（または空） |
| `null` に対する扱い | `null.equals(...)` で例外 | `Optional.empty()` はOK |
| 中身が `null` | 比較できない（例外） | `Optional.ofNullable(null)` は非推奨、`Optional.empty()` を使うべき |
| よくある用途 | 文字列比較 | Nullチェックを含む安全な値比較 |

---

###  実用的な注意点

####  危険パターン

```java
String str = null;
if (str.equals("test")) { ... } // ❌ NullPointerException
```

#### 安全な書き方

```java
if ("test".equals(str)) { ... } // ⭕ 安全（リテラルを左に）
```

または `Optional` を使って：

```java
Optional<String> opt = Optional.ofNullable(str);
if (opt.isPresent() && opt.get().equals("test")) { ... }
```

---

##  まとめ

- `String.equals()` は **内容を比較**。`null` に注意！
- `Optional.equals()` は **中身が等しいか**を比較。`empty()` 同士は等しい。
- `Optional` を使うことで、**Nullの安全性が大きく向上**します。

---
 `Objects.equals(Object a, Object b)` メソッドでは、**`null` 同士の比較は `true`** になります。

### 詳しく解説すると：

`Objects.equals(a, b)` の内部実装は以下のようになっています：

```java
public static boolean equals(Object a, Object b) {
    return (a == b) || (a != null && a.equals(b));
}
```

この実装を見ると：

- `a == b` が最初に評価されます。ここで `a` と `b` の両方が `null` の場合、`true` になります。
- どちらか一方が `null` で、もう一方が `null` でない場合は `false`
- 両方が `null` でない場合は `a.equals(b)` の結果が返されます

### 例：

```java
System.out.println(Objects.equals(null, null));     // true
System.out.println(Objects.equals(null, "abc"));    // false
System.out.println(Objects.equals("abc", null));    // false
System.out.println(Objects.equals("abc", "abc"));   // true
```

つまり、`null` 同士でも安全に比較できるのが `Objects.equals` のメリットですね。


