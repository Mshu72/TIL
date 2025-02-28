## **Java Stream API の `flatMap` メソッドとは？**

### **1. `flatMap` の基本概念**
`flatMap` は、**ストリームの各要素を別のストリームに変換し、それらを1つのストリームに統合するメソッド** です。

通常の `map` メソッドとの違いは以下の通りです。

| メソッド | 変換結果 |
|----------|-----------|
| `map` | 各要素を変換して、**そのまま新しい要素に置き換える** |
| `flatMap` | 各要素を **ストリームに変換し、それらを1つのストリームに統合する** |

---

### **2. `flatMap` の基本的な使い方**
以下の例で `map` と `flatMap` の違いを確認してみましょう。

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class FlatMapExample {
    public static void main(String[] args) {
        List<List<String>> listOfLists = List.of(
            List.of("A", "B", "C"),
            List.of("D", "E"),
            List.of("F", "G", "H")
        );

        // map を使う場合（リストのリストになる）
        List<Stream<String>> mapped = listOfLists.stream()
            .map(List::stream)
            .collect(Collectors.toList());
        System.out.println("map: " + mapped); // ストリームのリストになる

        // flatMap を使う場合（要素が1つのリストに統合される）
        List<String> flattened = listOfLists.stream()
            .flatMap(List::stream)
            .collect(Collectors.toList());
        System.out.println("flatMap: " + flattened);
    }
}
```

**出力結果**
```
map: [java.util.stream.ReferencePipeline$Head@1b6d3586, java.util.stream.ReferencePipeline$Head@4554617c, java.util.stream.ReferencePipeline$Head@74a14482]
flatMap: [A, B, C, D, E, F, G, H]
```

- **`map` を使うと `Stream<String>` のリスト（`List<Stream<String>>`）になってしまい、直接データを扱えない。**
- **`flatMap` を使うと `Stream<String>` に統合され、すべての要素を1つのリストにまとめることができる。**

---

### **3. `flatMap` の活用例**
#### **(1) リストのリストを1つのリストに統合**
```java
List<List<Integer>> listOfLists = List.of(
    List.of(1, 2, 3),
    List.of(4, 5),
    List.of(6, 7, 8)
);

List<Integer> flattenedList = listOfLists.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());

System.out.println(flattenedList); // [1, 2, 3, 4, 5, 6, 7, 8]
```
> **ポイント**: `flatMap` によって、ネストされたリストが1つのリストに統合される。

---

#### **(2) `flatMap` で文字列を分割してフラット化**
```java
List<String> sentences = List.of("Hello World", "Java Stream API", "flatMap example");

List<String> words = sentences.stream()
    .flatMap(sentence -> Stream.of(sentence.split(" ")))
    .collect(Collectors.toList());

System.out.println(words); // [Hello, World, Java, Stream, API, flatMap, example]
```
> **ポイント**: `split(" ")` により `Stream<String[]>` ができるが、`flatMap` でフラット化され `Stream<String>` になる。

---

#### **(3) `Optional` の `flatMap` を使ってネストを防ぐ**
```java
import java.util.Optional;

public class OptionalFlatMapExample {
    public static void main(String[] args) {
        Optional<String> optional = Optional.of("Hello");

        // map の場合: Optional<Optional<Integer>>
        Optional<Optional<Integer>> mapResult = optional.map(s -> Optional.of(s.length()));

        // flatMap の場合: Optional<Integer>
        Optional<Integer> flatMapResult = optional.flatMap(s -> Optional.of(s.length()));

        System.out.println("map result: " + mapResult);       // Optional[Optional[5]]
        System.out.println("flatMap result: " + flatMapResult); // Optional[5]
    }
}
```
> **ポイント**: `map` を使うと `Optional<Optional<T>>` になってしまうが、`flatMap` を使うと `Optional<T>` になる。

---

### **4. `flatMap` の流れ**
次のようなデータ構造を想定します。

```java
List<Map<String, Object>> branchMainGrouped;
List<Map<String, Object>> pwmgMainArea;
```

#### **(1) `map` を使った場合**
```java
List<Stream<Map<String, Object>>> mappedList = branchMainGrouped.stream()
    .map(branch -> pwmgMainArea.stream()
        .filter(pwmgArea -> Objects.equals(branch.get("EQP_ID"), pwmgArea.get("EQP_ID")))
    )
    .collect(Collectors.toList());
```
> **問題点**: `List<Stream<Map<String, Object>>>` になり、ストリームがネストされてしまう。

#### **(2) `flatMap` を使った場合**
```java
List<Map<String, Object>> flattenedList = branchMainGrouped.stream()
    .flatMap(branch -> pwmgMainArea.stream()
        .filter(pwmgArea -> Objects.equals(branch.get("EQP_ID"), pwmgArea.get("EQP_ID")))
    )
    .collect(Collectors.toList());
```
> **解決策**: `flatMap` により `Stream<Map<String, Object>>` になり、リストに直接格納できる。

---

## **5. `flatMap` のまとめ**
| 項目 | 説明 |
|------|------|
| **目的** | ストリームの各要素を新しいストリームに変換し、それらを1つのストリームに統合する。 |
| **`map` との違い** | `map` は1対1の変換、`flatMap` は1対多の変換（ストリームの統合）。 |
| **主な用途** | リストのリストの統合、文字列の分割、Optional のネスト解消、複雑なデータ処理。 |

### **`flatMap` のポイント**
1. **ネストされた構造をフラットにする**（例: `List<List<T>>` → `List<T>`）。
2. **複数のストリームを1つにまとめる**（例: `Stream<Stream<T>>` → `Stream<T>`）。
3. **データの変換とフィルタリングを組み合わせて効率的に処理できる**。

