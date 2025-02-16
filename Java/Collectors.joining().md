### **`Collectors.joining()` メソッドについて**
`Collectors.joining()` は Java の `Stream API` の `collect()` メソッドと組み合わせて使われる `Collector` であり、`Stream<String>` の要素を 1 つの文字列として結合するために使用されます。

### **基本構文**
`Collectors.joining()` は以下の 3 つのオーバーロードされたバージョンを持っています。

```java
// (1) 区切り文字なしで結合
Collectors.joining()

// (2) 指定した区切り文字で結合
Collectors.joining(CharSequence delimiter)

// (3) 区切り文字・開始文字・終了文字を指定して結合
Collectors.joining(CharSequence delimiter, CharSequence prefix, CharSequence suffix)
```

---

## **1. `Collectors.joining()`（区切り文字なし）**
各要素を**そのまま結合**します。

```java
List<String> words = Arrays.asList("Hello", "World");
String result = words.stream().collect(Collectors.joining());
System.out.println(result);  // 出力: "HelloWorld"
```

---

## **2. `Collectors.joining(delimiter)`（区切り文字を指定）**
要素を**指定した区切り文字で結合**します。

```java
List<String> words = Arrays.asList("apple", "banana", "cherry");
String result = words.stream().collect(Collectors.joining(", "));
System.out.println(result);  // 出力: "apple, banana, cherry"
```

- `", "` の部分が各単語の間に挿入される。

---

## **3. `Collectors.joining(delimiter, prefix, suffix)`（開始・終了文字を指定）**
**区切り文字だけでなく、開始文字と終了文字も指定**できます。

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
String result = names.stream().collect(Collectors.joining(", ", "[", "]"));
System.out.println(result);  // 出力: "[Alice, Bob, Charlie]"
```

- **`,`** → 各単語の区切り文字
- **`[`** → 開始文字（プレフィックス）
- **`]`** → 終了文字（サフィックス）

---

## **4. `Collectors.joining()` の応用例**
### **(1) 数値リストの結合**
数値のリストを `Stream<String>` に変換して、`joining()` で結合できます。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
String result = numbers.stream()
                        .map(String::valueOf)  // Integer → String に変換
                        .collect(Collectors.joining("-"));
System.out.println(result);  // 出力: "1-2-3-4-5"
```

---

### **(2) 空リストの場合**
空のリストに対して `Collectors.joining()` を使うと、空文字列 (`""`) が返ります。

```java
List<String> emptyList = new ArrayList<>();
String result = emptyList.stream().collect(Collectors.joining(", "));
System.out.println(result);  // 出力: ""
```

---

### **(3) 重複を除外して結合**
`distinct()` を使うことで、重複する要素を取り除いた上で結合できます。

```java
List<String> items = Arrays.asList("apple", "banana", "apple", "cherry");
String result = items.stream().distinct().collect(Collectors.joining(", "));
System.out.println(result);  // 出力: "apple, banana, cherry"
```

---

### **まとめ**
| バージョン | 説明 | 例 |
|-----------|---------------------------|----------------------------|
| `Collectors.joining()` | そのまま結合 | `"HelloWorld"` |
| `Collectors.joining(", ")` | 区切り文字を指定 | `"apple, banana, cherry"` |
| `Collectors.joining(", ", "[", "]")` | 区切り・開始・終了を指定 | `"[Alice, Bob, Charlie]"` |

`Collectors.joining()` を使うことで、リストや配列の要素を簡単に結合でき、可読性が向上します。
