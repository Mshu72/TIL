Javaの`Stream#peek`メソッドについて解説します。

### **1. `peek`メソッドとは？**
`peek`は **中間操作 (intermediate operation)** の一つで、各要素に対して動作を適用しつつ、その要素をそのまま返すメソッドです。  
主に **デバッグ目的** で使用され、ストリームの流れの途中で要素の状態を確認できます。

#### **peekメソッドのシグネチャ**
```java
Stream<T> peek(Consumer<? super T> action)
```
- `action`: 各要素に対して適用する処理（副作用を持つ関数 `Consumer`）
- **戻り値**: 処理された `Stream` をそのまま返す（変更しない）

---

### **2. peekの使い方**
#### **(1) デバッグに利用**
例えば、`map` や `filter` などのストリーム処理の途中で値を確認したい場合に使えます。

```java
import java.util.stream.Stream;

public class PeekExample {
    public static void main(String[] args) {
        Stream.of("apple", "banana", "cherry")
                .filter(s -> s.startsWith("a"))   // "apple" だけが残る
                .peek(s -> System.out.println("Filtered: " + s))
                .map(String::toUpperCase)         // "APPLE" に変換
                .peek(s -> System.out.println("Mapped: " + s))
                .forEach(System.out::println);    // 最終結果を出力
    }
}
```

**出力結果**
```
Filtered: apple
Mapped: APPLE
APPLE
```
このように、`peek` を使うことでストリームの各段階でデータがどのように処理されているかを確認できます。

---

### **3. `forEach`との違い**
- `peek` は **中間操作** で、ストリームをそのまま返す  
- `forEach` は **終端操作 (terminal operation)** で、ストリームを消費して処理を完了する

```java
Stream.of(1, 2, 3, 4, 5)
    .peek(System.out::println) // 各要素を出力しつつ、ストリームを流れる
    .map(n -> n * 2) 
    .forEach(System.out::println); // 変換後の値を出力
```

**出力**
```
1
2
3
4
5
2
4
6
8
10
```
`peek` は `map` の前に実行されていることがわかります。

---

### **4. peekを使う際の注意点**
#### **(1) 副作用のある処理をするとバグの原因になりやすい**
`peek` は基本的にデバッグ用であり、副作用のある処理（リストの変更や変数の変更など）には向いていません。

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

public class PeekSideEffect {
    public static void main(String[] args) {
        List<String> result = new ArrayList<>();
        
        Stream.of("A", "B", "C")
              .peek(result::add) // ストリームの途中でリストに追加
              .forEach(System.out::println);
        
        System.out.println("Result List: " + result);
    }
}
```

**期待される動作**  
`result` に `["A", "B", "C"]` が入ると思いがちですが、**ストリームが遅延評価** されるため、最適化によって `peek` が実行されないことがあります。

> **解決策:** `peek` ではなく `forEach` で確実に処理を行う

```java
Stream.of("A", "B", "C")
      .forEach(result::add);
```

#### **(2) `peek` を終端操作なしで使うと実行されない**
```java
Stream.of(1, 2, 3)
    .peek(System.out::println); // 何も出力されない
```
ストリームは **終端操作 (`forEach`, `collect`, `count`, etc.)** を呼び出さないと実行されないため、上記コードは何も実行されません。

---

### **5. まとめ**
✅ `peek` はストリームの中間操作で、主に **デバッグ目的** で使う  
✅ `peek` を使うとストリーム処理の途中で要素を確認できる  
✅ `forEach` とは異なり、終端操作がないと `peek` は実行されない  
✅ `peek` を副作用のある処理に使うとバグの原因になりやすい  

**💡 推奨:** デバッグ用途以外では `peek` を使わず、`map` や `forEach` を適切に使うのが良い！
