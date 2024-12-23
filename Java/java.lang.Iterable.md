`java.lang.Iterable` を実装するクラスは、**そのクラスのオブジェクトが反復処理（イテレーション）可能になる**ことを意味します。つまり、そのクラスは`for-each`ループや`Iterator`を使って要素を順番に処理できるようになります。

### `Iterable` インターフェースの概要
```java
public interface Iterable<T> {
    Iterator<T> iterator();
}
```
- `T` はイテレートする要素の型です。  
- `iterator()` メソッドは、コレクションの要素を順番に返す`Iterator`オブジェクトを提供します。  

### `Iterable` を実装する代表的なクラス
- **`ArrayList`**
- **`HashSet`**
- **`LinkedList`**
- **`HashMap#keySet()` や `values()`** などのコレクションビュー
- **`TreeSet`**
- **`PriorityQueue`**

これらは`Iterable`を実装しているため、以下のように`for-each`ループで要素を処理できます。
```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

for (String item : list) {
    System.out.println(item);
}
```

### カスタムクラスで`Iterable`を実装する例
自分で`Iterable`を実装したクラスを作成し、反復処理を可能にする例を示します。

```java
import java.util.Iterator;
import java.util.NoSuchElementException;

public class MyCollection<T> implements Iterable<T> {
    private T[] data;
    private int size = 0;

    public MyCollection(int capacity) {
        data = (T[]) new Object[capacity];
    }

    public void add(T item) {
        if (size < data.length) {
            data[size++] = item;
        }
    }

    @Override
    public Iterator<T> iterator() {
        return new MyIterator();
    }

    private class MyIterator implements Iterator<T> {
        private int index = 0;

        @Override
        public boolean hasNext() {
            return index < size;
        }

        @Override
        public T next() {
            if (!hasNext()) {
                throw new NoSuchElementException();
            }
            return data[index++];
        }
    }
}
```

#### 使用例
```java
public class Main {
    public static void main(String[] args) {
        MyCollection<String> collection = new MyCollection<>(5);
        collection.add("Apple");
        collection.add("Banana");
        collection.add("Cherry");

        for (String item : collection) {
            System.out.println(item);
        }
    }
}
```

### ポイント
- `iterator()` メソッドで独自の`Iterator`を返すことで、反復処理のロジックを自由にカスタマイズできます。
- `Iterator`は`hasNext()`で次の要素の存在を確認し、`next()`で要素を返します。
- `Iterable`を実装することで、クラスがより直感的に使用でき、Java標準のコレクションと同じように`for-each`ループが使えるようになります。

### メリット
- コードの簡潔性が向上
- 内部実装を隠蔽し、イテレーション方法を柔軟にカスタマイズ可能
- `Stream`APIなどでも利用できる

必要に応じて`remove()`メソッドを追加して、要素の削除機能を`Iterator`に組み込むこともできます。
