###  **`LinkedList` でよく使われるメソッド一覧 (Java)**

`LinkedList` は **`List`**、**`Deque`**、**`Queue`** インターフェースを実装しているため、多用途に使用できます。  
ここでは、**実用的かつ頻繁に使われるメソッド**をカテゴリ別に紹介します。

---

##  **1. 要素の追加 (Add Operations)**

| メソッド                | 説明                                     | 戻り値     |
|----------------------|----------------------------------------|----------|
| `add(E e)`          | リストの末尾に要素を追加。                      | `boolean` |
| `add(int index, E e)` | 指定した位置に要素を追加。                      | `void`   |
| `addFirst(E e)`     | リストの先頭に要素を追加。                      | `void`   |
| `addLast(E e)`      | リストの末尾に要素を追加。 (`add(e)` と同じ)       | `void`   |
| `offer(E e)`        | キューの末尾に要素を追加。 (キューとして使用する場合) | `boolean` |
| `offerFirst(E e)`   | キューの先頭に要素を追加。                     | `boolean` |
| `offerLast(E e)`    | キューの末尾に要素を追加。                     | `boolean` |

###  **使用例:**
```java
LinkedList<String> list = new LinkedList<>();
list.add("Java");
list.addFirst("C++");
list.addLast("Python");
System.out.println(list); // [C++, Java, Python]
```

---

##  **2. 要素の取得 (Access Operations)**

| メソッド              | 説明                            | 戻り値       |
|-------------------|-------------------------------|------------|
| `get(int index)`  | 指定したインデックスの要素を取得。        | `E`        |
| `getFirst()`      | 最初の要素を取得。                 | `E`        |
| `getLast()`       | 最後の要素を取得。                 | `E`        |
| `peek()`          | 最初の要素を取得（削除はしない）。     | `E` または `null` |
| `peekFirst()`     | 最初の要素を取得（削除はしない）。     | `E` または `null` |
| `peekLast()`      | 最後の要素を取得（削除はしない）。     | `E` または `null` |

###  **使用例:**
```java
System.out.println(list.getFirst()); // C++
System.out.println(list.getLast());  // Python
System.out.println(list.get(1));     // Java
```

---

##  **3. 要素の削除 (Remove Operations)**

| メソッド                | 説明                                      | 戻り値       |
|----------------------|-----------------------------------------|------------|
| `remove()`          | 最初の要素を削除して返す。                      | `E`        |
| `remove(int index)` | 指定したインデックスの要素を削除して返す。          | `E`        |
| `remove(Object o)`  | 最初に出現する指定要素を削除する。               | `boolean`  |
| `removeFirst()`     | 最初の要素を削除して返す。                     | `E`        |
| `removeLast()`      | 最後の要素を削除して返す。                     | `E`        |
| `poll()`            | 最初の要素を削除して返す（キュー用）。            | `E` または `null` |
| `pollFirst()`       | 最初の要素を削除して返す（キュー用）。            | `E` または `null` |
| `pollLast()`        | 最後の要素を削除して返す（キュー用）。            | `E` または `null` |

###  **使用例:**
```java
list.removeFirst();  // C++ を削除
list.removeLast();   // Python を削除
System.out.println(list); // [Java]
```

---

##  **4. スタック操作 (Stack Operations)**

`LinkedList` は `Deque` インターフェースを実装しているため、**スタック (LIFO: Last In, First Out)** としても利用できます。

| メソッド       | 説明                   | 戻り値   |
|------------|----------------------|--------|
| `push(E e)` | 要素をスタックのトップに追加。    | `void` |
| `pop()`     | スタックのトップの要素を削除して返す。 | `E`    |
| `peek()`    | スタックのトップの要素を取得。    | `E`    |

###  **使用例:**
```java
LinkedList<Integer> stack = new LinkedList<>();
stack.push(100);
stack.push(200);
stack.push(300);
System.out.println(stack.pop()); // 300
System.out.println(stack.peek()); // 200
```

---

##  **5. キュー操作 (Queue Operations)**

`LinkedList` は **キュー (FIFO: First In, First Out)** としても利用可能です。

| メソッド           | 説明                         | 戻り値       |
|----------------|----------------------------|------------|
| `offer(E e)`  | キューの末尾に要素を追加。         | `boolean`  |
| `poll()`      | 最初の要素を取得して削除。         | `E` または `null` |
| `peek()`      | 最初の要素を取得（削除はしない）。    | `E` または `null` |

###  **使用例:**
```java
LinkedList<String> queue = new LinkedList<>();
queue.offer("A");
queue.offer("B");
queue.offer("C");
System.out.println(queue.poll()); // A
System.out.println(queue.peek()); // B
```

---

##  **6. 検索 (Search Operations)**

| メソッド                  | 説明                       | 戻り値     |
|-----------------------|--------------------------|----------|
| `contains(Object o)` | リストに指定した要素が含まれているか確認。 | `boolean` |
| `indexOf(Object o)`  | 最初に出現する要素のインデックスを返す。   | `int`    |
| `lastIndexOf(Object o)` | 最後に出現する要素のインデックスを返す。 | `int`    |

###  **使用例:**
```java
System.out.println(list.contains("Java"));   // true
System.out.println(list.indexOf("Python"));  // インデックスを返すか、-1
```

---

##  **7. その他便利なメソッド**

| メソッド              | 説明                          | 戻り値    |
|-------------------|-----------------------------|---------|
| `clear()`        | リストの全要素を削除。              | `void`  |
| `isEmpty()`      | リストが空かどうか確認。              | `boolean` |
| `size()`         | リストの要素数を取得。               | `int`   |
| `clone()`        | `LinkedList` の浅いコピーを返す。     | `Object`|

###  **使用例:**
```java
System.out.println(list.size());      // 要素数を出力
System.out.println(list.isEmpty());   // 空かどうかを判定
list.clear();                         // 全要素削除
```

---

##  **まとめ: よく使われるメソッドTOP10**  
1. `add(E e)` – 要素の追加  
2. `addFirst(E e)` / `addLast(E e)` – 先頭/末尾への追加  
3. `get(int index)` – インデックスで要素取得  
4. `getFirst()` / `getLast()` – 先頭/末尾要素取得  
5. `remove()` / `removeFirst()` / `removeLast()` – 要素削除  
6. `peek()` / `peekFirst()` / `peekLast()` – キュー操作向け取得  
7. `push(E e)` / `pop()` – スタック操作  
8. `offer(E e)` / `poll()` – キュー操作  
9. `contains(Object o)` – 要素の存在確認  
10. `size()` / `isEmpty()` – リストの状態確認  

---

##  **結論:**
`LinkedList` は、**多用途なデータ構造**としてリスト、キュー、スタックの動作をサポートします。  
- 頻繁な挿入・削除操作が必要な場合に適しており、  
- `ArrayList` よりも柔軟な構造を持ちますが、**ランダムアクセス**が必要な場合は `ArrayList` の方が効率的です。  
