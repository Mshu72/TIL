`.size()` メソッドは、Javaのコレクションフレームワークで使われるメソッドで、コレクション内に含まれる要素の数を返します。このメソッドは、**リスト（`List`）** や **セット（`Set`）**、その他のコレクションでよく利用されます。

---

## **1. 使用目的**
- コレクション（`List`、`Set`、`Map` など）の要素数（サイズ）を取得するために使用します。

---

## **2. 対応するクラス・インターフェース**
`.size()` メソッドは、`Collection` インターフェースで定義されており、そのすべての実装クラスで利用できます。

代表的なクラス：
| クラス/インターフェース | 説明                               |
|-------------------------|------------------------------------|
| `List`                 | 順序付きコレクション              |
| `Set`                  | 重複を許さないコレクション         |
| `Map`                  | キーと値のペアを管理するコレクション |

---

## **3. メソッドのシグネチャ**

```java
int size()
```

- **戻り値:** コレクションに含まれる要素の数を `int` 型で返します。
- **例外:** このメソッド自体は例外をスローしません。ただし、コレクションが正しく初期化されていない場合、`NullPointerException` が発生する可能性があります。

---

## **4. 使用例**

### **例1: リストでの使用**
```java
import java.util.ArrayList;
import java.util.List;

public class SizeExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        System.out.println("List size: " + list.size()); // 出力: List size: 3
    }
}
```

### **例2: セットでの使用**
```java
import java.util.HashSet;
import java.util.Set;

public class SizeExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Dog");
        set.add("Cat");
        set.add("Bird");

        System.out.println("Set size: " + set.size()); // 出力: Set size: 3
    }
}
```

### **例3: マップでの使用**
```java
import java.util.HashMap;
import java.util.Map;

public class SizeExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("Alice", 25);
        map.put("Bob", 30);

        System.out.println("Map size: " + map.size()); // 出力: Map size: 2
    }
}
```

---

## **5. 特徴と注意点**

### **1. パフォーマンス**
- `.size()` メソッドのパフォーマンスは、コレクションの実装によって異なります。
  - **`ArrayList`**: 要素数を内部で保持しているため、計算不要で高速。
  - **`LinkedList`**: 同様に、サイズを保持しており高速。
  - **`HashSet` / `HashMap`**: サイズを管理しているため、高速。
  - **特殊なコレクション**: サイズ計算に時間がかかる場合もある（例：大規模データや非同期ストリームなど）。

---

### **2. 空のコレクションの場合**
- 空のコレクションで `.size()` を呼び出すと、`0` を返します。
```java
List<String> list = new ArrayList<>();
System.out.println(list.size()); // 出力: 0
```

---

### **3. Null の場合**
- コレクションが `null` の場合、`.size()` を呼び出すと **`NullPointerException`** が発生します。
```java
List<String> list = null;
System.out.println(list.size()); // 例外: NullPointerException
```

**解決策:**
- `null` チェックを行う。
```java
if (list != null) {
    System.out.println("Size: " + list.size());
} else {
    System.out.println("The list is null.");
}
```

---

## **6. `.length` や `.length()` との違い**
Javaでは、`.size()` 以外にも配列や文字列で長さを取得する方法がありますが、それぞれの用途が異なります。

| メソッド名        | 使用対象              | 例                                      |
|-------------------|-----------------------|-----------------------------------------|
| `.size()`         | コレクション          | `list.size()`                          |
| `.length`         | 配列                  | `array.length`                         |
| `.length()`       | 文字列（`String`）    | `"hello".length()`                     |

---

## **7. まとめ**
- `.size()` はコレクション内の要素数を取得するために使われます。
- 空のコレクションでは `0` を返しますが、コレクションが `null` の場合は例外が発生します。
- `ArrayList` や `HashSet`、`HashMap` など、コレクションの種類を問わず使用可能です。
- 配列や文字列の長さを取得したい場合は、それぞれ `.length` や `.length()` を使用する必要があります。

[チャットGPT 無料、登録なし](https://www.google.co.jp/search?q=gptjp.net)
