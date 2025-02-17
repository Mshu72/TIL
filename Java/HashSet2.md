## **`HashSet` とは？**
`HashSet` は Java の `Set` インターフェースを実装したクラスの一つで、**重複を許さず、順序を保証しないコレクション** です。内部的に `HashMap` を使用しており、高速なデータ検索 (`contains`) や追加 (`add`) 操作が可能です。

---

## **`HashSet` の特徴**
1. **重複を許さない**
   - `Set` の特性として、同じ値を複数回追加しても、一つしか格納されません。
2. **要素の順序は保証されない**
   - `HashSet` は `HashMap` を内部的に使用するため、要素の挿入順が保持されません。
3. **高速な検索・追加・削除が可能**
   - 平均的な時間計算量は **O(1)**（ほぼ一定時間）で動作します。
4. **`null` を 1 つだけ格納できる**
   - `null` の要素を 1 つだけ持つことができます。

---

## **`HashSet` の使い方**

### **1. 基本的な操作**
```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> fruits = new HashSet<>();

        // 要素の追加
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        fruits.add("Apple"); // 重複 → 無視される

        // 出力
        System.out.println(fruits); // [Banana, Orange, Apple] ※順序は保証されない

        // 要素の検索
        System.out.println(fruits.contains("Banana")); // true
        System.out.println(fruits.contains("Grape")); // false

        // 要素の削除
        fruits.remove("Banana");
        System.out.println(fruits); // [Orange, Apple]
        
        // 要素数
        System.out.println(fruits.size()); // 2

        // すべての要素を削除
        fruits.clear();
        System.out.println(fruits.isEmpty()); // true
    }
}
```

---

### **2. `null` の格納**
```java
Set<String> set = new HashSet<>();
set.add(null);
set.add("Hello");
set.add(null); // 2回目の null は無視される
System.out.println(set); // [null, Hello]
```
→ `null` は **1 つだけ** 保持される。

---

### **3. `HashSet` の繰り返し処理**
`HashSet` は順序を保証しないため、要素の順番が変わることがあります。

#### **拡張 for ループ**
```java
Set<String> set = new HashSet<>();
set.add("Dog");
set.add("Cat");
set.add("Bird");

for (String s : set) {
    System.out.println(s);
}
```

#### **Iterator を使用**
```java
import java.util.Iterator;
import java.util.HashSet;
import java.util.Set;

public class HashSetIteratorExample {
    public static void main(String[] args) {
        Set<Integer> numbers = new HashSet<>();
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);

        Iterator<Integer> iterator = numbers.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

---

### **4. `List` から `HashSet` を作成（重複排除）**
`HashSet` を使うと、`List` 内の **重複を削除** できます。

```java
import java.util.*;

public class ListToHashSet {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("A", "B", "A", "C", "B");
        Set<String> uniqueSet = new HashSet<>(list);

        System.out.println(uniqueSet); // [A, B, C]（順不同）
    }
}
```

---

## **`HashSet` の内部構造**
### **1. 内部的には `HashMap` を使用**
`HashSet` は `HashMap` のキー (`key`) のみを利用し、値 (`value`) には固定のダミー値 (`private static final Object PRESENT = new Object();`) が入ります。

```java
private transient HashMap<E,Object> map;
private static final Object PRESENT = new Object();
```

例えば、次の `HashSet`:
```java
HashSet<String> set = new HashSet<>();
set.add("apple");
set.add("banana");
```
内部的には、次の `HashMap` が作成されます：
```java
{ "apple" => PRESENT, "banana" => PRESENT }
```

### **2. `add()` の仕組み**
- `add()` メソッドは、内部の `HashMap` にキーを登録する形で動作します。
- **キーが既に存在する場合は追加されない**（重複防止）。

```java
public boolean add(E e) {
    return map.put(e, PRESENT) == null;
}
```

---

## **`HashSet` と `TreeSet`・`LinkedHashSet` の違い**
| クラス | 内部構造 | 順序 | 速度 |
|--------|---------|------|------|
| `HashSet` | `HashMap` | 順序なし | 高速 (O(1)) |
| `LinkedHashSet` | `LinkedHashMap` | **追加順を維持** | やや遅い |
| `TreeSet` | `TreeMap` | **ソートされた順** | O(log n)（`Red-Black Tree` を使用） |

---

## **`HashSet` を使うべき場合**
✅ **重複を排除したいが、順番は気にしないとき**  
✅ **高速な追加・削除・検索が必要なとき**（`O(1)` の操作速度）

### **`HashSet` を避けるべき場合**
❌ **順番を保持したいとき** → `LinkedHashSet`  
❌ **ソートされた順序が必要なとき** → `TreeSet`

---

## **まとめ**
- `HashSet` は **重複を許さない** `Set` の一種で、`HashMap` を内部的に使用。
- **順序は保証されない** ため、順番が必要な場合は `LinkedHashSet` か `TreeSet` を使う。
- **追加・削除・検索は高速 (`O(1)`)** なので、**重複排除** や **高速検索** に適している。

使う場面によって `HashSet`、`LinkedHashSet`、`TreeSet` を使い分けましょう！
