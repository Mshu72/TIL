Java 24（2024年リリース予定）の新機能の一つである **`StreamGatherers`** は、`Stream` API を拡張して、より柔軟で強力な集約処理を可能にする新しい仕組みです。

---

##  **StreamGatherersとは？**

**`StreamGatherers`** は、`java.util.stream` パッケージに追加された新しいユーティリティで、**ストリームの中間処理における複雑な状態管理や制御**をより簡単に、かつ効率的に行うことができます。

従来の `Stream` API では難しかった「複雑な状態遷移を含む処理」や「複数の要素を1つの処理単位にまとめる」ような場面で役立ちます。

---

##  **主な機能**

- **状態を持った中間操作**
  - 状態を維持しながらストリームを処理できる（例：一定数の要素ごとにグループ化）
  
- **カスタムなデータ集約**
  - 通常の `.map()` や `.flatMap()` では表現しづらいロジックを簡潔に記述可能
  
- **`takeWhile` や `dropWhile` のような処理の柔軟化**

---

##  使用例

```java
import java.util.stream.Stream;
import java.util.stream.StreamGatherers;

List<List<Integer>> grouped = Stream.of(1, 2, 3, 4, 5, 6, 7)
    .gather(StreamGatherers.windowFixed(3))
    .toList();

System.out.println(grouped); 
// 出力: [[1, 2, 3], [4, 5, 6], [7]]
```

この例では、3つずつの固定サイズでリストがグループ化されます。

---

##  どんなときに使える？

- ローリング平均や移動ウィンドウ処理
- 要素のバッチ処理
- 条件に応じたストリームの切断・集約

---

Streamでは、前の値を参照するような処理や、処理順序を前提とした処理が行えません。そのため、前の値にどんどん手を加えてリストを作ったり、移動平均をとったりといったことができませんでした。
そういった、順番を保証して前の値を踏まえた処理が行えるようにするのが、Gathererです。

デザインノートはこちら
https://cr.openjdk.org/~vklang/Gatherers.html

Collectorと同じで自前のGathererを実装するのは大変そうですが、CollectorsのようにGatherersが用意されています。ここでは、Gatherersだけ紹介します。

Streamが使えそうで使えなかった処理に、Streamが使える場合が増えそうです。
