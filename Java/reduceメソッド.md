Javaの `Stream` API にある `reduce` メソッドは、ストリームの要素を集約（リダクション）するための強力な機能を提供します。これは、ストリームの要素を1つの結果にまとめる際に使用されます。

## `reduce` メソッドのオーバーロード
`reduce` メソッドには、以下の3つのオーバーロードがあります。

### 1. **初期値を持つ reduce**
```java
T reduce(T identity, BinaryOperator<T> accumulator)
```
- **identity**: 初期値（例: 0, "", new Object() など）
- **accumulator**: 2つの要素を統合する関数

#### 例: 数値の合計を求める
```java
import java.util.Arrays;
import java.util.List;

public class ReduceExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        int sum = numbers.stream().reduce(0, (a, b) -> a + b);
        System.out.println(sum); // 出力: 15
    }
}
```
この場合、`0` は初期値で、`(a, b) -> a + b` でリストのすべての要素を加算します。

---

### 2. **初期値なしの reduce**
```java
Optional<T> reduce(BinaryOperator<T> accumulator)
```
- **accumulator**: 2つの要素を統合する関数
- **戻り値**: ストリームが空の場合 `Optional.empty()` を返す

#### 例: 最大値を求める
```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class ReduceExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(3, 5, 2, 8, 7);
        Optional<Integer> max = numbers.stream().reduce((a, b) -> a > b ? a : b);
        max.ifPresent(System.out::println); // 出力: 8
    }
}
```
この場合、ストリームが空だと `Optional.empty()` になるため、`ifPresent()` で安全に処理できます。

---

### 3. **並列ストリーム対応（3引数の reduce）**
```java
<U> U reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)
```
- **identity**: 初期値
- **accumulator**: 各要素を処理する関数
- **combiner**: 並列処理時に部分結果を統合する関数（`parallelStream()` で有効）

#### 例: 文字列の結合（並列処理）
```java
import java.util.Arrays;
import java.util.List;

public class ReduceExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("Hello", "World", "Java", "Stream");

        String result = words.parallelStream().reduce(
            "",  // 初期値
            (s1, s2) -> s1 + s2,  // 各要素を処理
            (s1, s2) -> s1 + s2   // 並列実行時に統合
        );

        System.out.println(result); // 出力: HelloWorldJavaStream
    }
}
```
この3引数バージョンは、並列ストリーム (`parallelStream()`) を使用した場合に `combiner` で部分結果を統合するのがポイントです。

---

## `reduce` と `collect` の違い
`reduce` は基本的に「単一の結果」に集約する場合に使いますが、要素の変換や集約には `collect` の方が適している場合があります。

#### 例: `reduce` でリストを結合する（非効率）
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ReduceExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "cherry");

        String result = words.stream().reduce("", (s1, s2) -> s1 + ", " + s2);
        System.out.println(result); // 出力: , apple, banana, cherry
    }
}
```
このような場合、`collect(Collectors.joining(", "))` の方が適しています。

#### `collect` を使うと効率的
```java
String result = words.stream().collect(Collectors.joining(", "));
System.out.println(result); // 出力: apple, banana, cherry
```

---

## まとめ
- `reduce(identity, accumulator)` → 初期値あり、要素を畳み込む
- `reduce(accumulator)` → 初期値なし、`Optional` を返す
- `reduce(identity, accumulator, combiner)` → 並列処理時の最適化
- 文字列やリストを集約する場合は `collect` の方が適している場合がある

使いどころを理解すると、ストリームをより効果的に活用できます！
