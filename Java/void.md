javaのvoidは、メソッドの戻り値の型がないことを示すキーワードです。  
つまり、そのメソッドが値を返さないことを意味します。  
以下はvoidに関する基本的なポイントです。

# voidの使い方
メソッドが何も値を返さずに処理を終える場合、そのメソッドの戻り値の型としてvoidを指定します。  
これにより、そのメソッドは計算や処理を行うものの、呼び出し元に何も返さずに終了します。

# 使用例
```java
public class Example {
    // 戻り値がないメソッド
    public void sayHello() {
        System.out.println("Hello!");
    }

    public static void main(String[] args) {
        Example example = new Example();
        example.sayHello();  // "Hello!"と出力されるが、何も返さない
    }
}
```
## ポイント
メソッドにvoidが指定されている場合、returnステートメントを使って値を返すことはできません。  
例えば、`int`や`String`などの型のメソッドとは異なり、`void`メソッドでは明示的に値を返す必要がないからです。  
ただし、`void`メソッドの中でも、`return`ステートメント自体を使ってメソッドを途中で終了させることは可能です。  
この場合、`return`キーワードの後に何も記述しません。
```java
public void earlyReturnExample() {
    System.out.println("Start of method");
    if (true) {
        return;  // ここでメソッドを終了する
    }
    System.out.println("This won't be printed");
}
```
# voidの適用範囲
主にメソッドの戻り値型として使われますが、`void`は変数やフィールドの型として使うことはできません。  










