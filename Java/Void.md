`void`は、**Javaにおけるメソッドの戻り値が存在しないことを示すキーワード**です。つまり、そのメソッドは何も値を返さず、処理だけを実行します。

---

##  **基本構文と使い方**

```java
public class Example {

    // 戻り値なしのメソッド
    public void greet() {
        System.out.println("Hello, World!");
    }

    public static void main(String[] args) {
        Example example = new Example();
        example.greet();  // "Hello, World!" と出力される
    }
}
```
- **解説**:  
  - `public void greet()`は、`greet`メソッドが何も返さないことを示しています。
  - `System.out.println()`は標準出力にメッセージを表示する処理を行いますが、戻り値は返しません。

---

##  **なぜ `void` を使うのか？**

1. **処理の実行が目的のとき**  
   例: データの表示、ファイルへの書き込み、データベースへの保存など。

2. **戻り値が不要な操作**  
   例: オブジェクトの状態を変更するだけのメソッド。

---

##  **voidメソッドと戻り値ありメソッドの違い**

```java
public class Calculator {

    // 戻り値がない (void) メソッド
    public void displayResult(int result) {
        System.out.println("結果は: " + result);
    }

    // 戻り値がある (int) メソッド
    public int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        int sum = calc.add(5, 3);   // 8を返す
        calc.displayResult(sum);   // "結果は: 8" と出力される
    }
}
```
- `displayResult`: 処理（表示）を実行するだけで、何も返さないため`void`を使用。
- `add`: 計算結果を返すため、戻り値の型として`int`を使用。

---

##  **注意点**
- `void`メソッド内で`return;`を使うことは可能ですが、**値を返す`return`は使えません**。

```java
public void process() {
    if (true) {
        return;  // ここでメソッドを終了する（値は返さない）
    }
    System.out.println("処理完了");
}
```

---

##  **`void`を使う場面の例**

### 1. **イベントハンドラー**
```java
public void onClick() {
    System.out.println("ボタンがクリックされました！");
}
```

### 2. **ロギング処理**
```java
public void log(String message) {
    System.out.println("ログ: " + message);
}
```

### 3. **システム処理のトリガー**
```java
public void startProcess() {
    initialize();
    execute();
    cleanup();
}
```

---

##  **まとめ**

| `void`メソッドの特徴         | 説明                                     |
|---------------------------|----------------------------------------|
| **戻り値**                | なし                                   |
| **使用目的**              | 処理の実行のみ（結果を返さない）               |
| **主な用途**              | ログ出力、状態更新、UI処理、ファイル書き込みなど |
| **`return`の使用**         | 値なしの`return;`でメソッドを途中終了できる    |

