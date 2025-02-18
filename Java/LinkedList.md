### **LinkedList の解説**
`LinkedList` は、Java の `java.util` パッケージに含まれる **双方向連結リスト (Doubly Linked List)** の実装です。  
`List` インターフェースと `Deque` インターフェースを実装しており、**リスト (List) とキュー (Queue) の両方として機能** します。

---

## **1. LinkedList の特徴**
### **(1) 内部構造**
- `LinkedList` は **ノード (Node)** と呼ばれる要素の集合で構成される。
- 各ノードは **「データ (値)」と「次のノードへの参照 (next)」「前のノードへの参照 (previous)」** を持つ。
- これにより、要素の追加・削除が **O(1) の計算量** で可能。

### **(2) 主な特徴**
| 特徴             | LinkedList | ArrayList |
|----------------|------------|------------|
| **データの格納方法** | ノード (前後のリンク付き) | 配列 (インデックスでアクセス) |
| **要素の追加/削除 (中間地点)** | **速い O(1)** (リンク変更のみ) | **遅い O(n)** (要素をずらす必要あり) |
| **要素の取得 (ランダムアクセス)** | **遅い O(n)** (先頭から順に検索) | **速い O(1)** (インデックスで直接アクセス) |
| **メモリ使用量** | **多い** (ノードごとに参照情報を保持) | **少ない** (データのみ保持) |

- **ArrayList はインデックスで直接アクセスできるため検索が速いが、途中の要素を追加・削除すると移動コストがかかる。**
- **LinkedList はノードの参照を変更するだけで要素の追加・削除ができるが、インデックスでのランダムアクセスが遅い。**

---

## **2. LinkedList の使いどころ**
### **✔ 向いているケース**
✅ **要素の追加・削除が頻繁に発生する場合**  
　→ `O(1)` で効率的に追加・削除できる。  
✅ **データの順序を保持しつつ、先頭や末尾の要素を操作したい場合**  
　→ `Deque` インターフェースを利用し、スタックやキューとして使える。  
✅ **大きなリストで、メモリ効率よりも挿入・削除速度を優先する場合**

### **❌ 向いていないケース**
❌ **頻繁にインデックスアクセス (検索) をする場合**  
　→ `O(n)` かかるため、`ArrayList` の方が圧倒的に速い。  
❌ **メモリ効率を優先したい場合**  
　→ 追加の参照情報を持つため、`ArrayList` よりメモリを消費する。  

---

## **3. LinkedList の基本操作**
### **(1) インスタンス生成**
```java
import java.util.LinkedList;
import java.util.List;

public class LinkedListExample {
    public static void main(String[] args) {
        // LinkedList の作成
        List<String> list = new LinkedList<>();

        // 要素の追加
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        // 出力
        System.out.println(list); // [Apple, Banana, Cherry]
    }
}
```

### **(2) 先頭・末尾への追加・削除**
```java
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        // 先頭に追加
        list.addFirst("First");
        // 末尾に追加
        list.addLast("Last");

        System.out.println(list); // [First, Last]

        // 先頭の要素を取得
        System.out.println(list.getFirst()); // First
        // 末尾の要素を取得
        System.out.println(list.getLast()); // Last

        // 先頭の要素を削除
        list.removeFirst();
        // 末尾の要素を削除
        list.removeLast();

        System.out.println(list); // []
    }
}
```

### **(3) 中間の要素を追加・削除**
```java
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        list.add("A");
        list.add("B");
        list.add("C");

        // インデックス 1 の位置に追加
        list.add(1, "X");

        System.out.println(list); // [A, X, B, C]

        // インデックス 2 の要素を削除
        list.remove(2);

        System.out.println(list); // [A, X, C]
    }
}
```

### **(4) ループ処理**
```java
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        list.add("One");
        list.add("Two");
        list.add("Three");

        // 拡張 for 文
        for (String item : list) {
            System.out.println(item);
        }

        // while + イテレータ
        var iterator = list.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

---

## **4. LinkedList と ArrayList の選択基準**
| **要件**                      | **適したコレクション** |
|------------------------------|------------------|
| 頻繁にデータを **追加・削除** する | **LinkedList** |
| 頻繁にデータを **検索** する    | **ArrayList** |
| **メモリ使用量を抑えたい**       | **ArrayList** |
| **FIFO (キュー)** のように使いたい | **LinkedList** |

---

## **5. まとめ**
- `LinkedList` は **要素の追加・削除に強いが、検索に弱い**。
- **ランダムアクセスを多用する場合は `ArrayList` を選ぶべき**。
- **リストとしてだけでなく、`Deque` (双方向キュー) の機能も持つ** ため、スタックやキューのように使うのにも適している。

💡 **使い分けのポイント:**  
- **大量のデータを扱い、途中の要素を頻繁に追加・削除するなら `LinkedList`**  
- **インデックスアクセスを多用するなら `ArrayList`**

`LinkedList` は適材適所で使えば強力なデータ構造ですが、無闇に使うと `ArrayList` よりパフォーマンスが悪くなることがあるので、用途に応じて選びましょう！ 🚀
