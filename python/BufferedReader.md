`BufferedReader` は、Javaの `java.io` パッケージに含まれるクラスで、入力ストリームをバッファリングすることで効率的な文字データの読み取りを可能にするクラスです。

---

## **1. `BufferedReader` の概要**
- **バッファリングによるパフォーマンス向上**  
  → 1文字ずつ直接読み込むのではなく、バッファにデータをまとめて読み込むことで、ファイルやネットワークからのデータ取得の速度を向上させる。

- **行単位での読み取りが可能**  
  → `readLine()` メソッドを使うと、一度に1行ずつテキストを読み込むことができる。

- **ストリームをラップして使用**  
  → `BufferedReader` は `Reader` のサブクラスなので、`FileReader` などの他の `Reader` クラスと組み合わせて使用する。

---

## **2. `BufferedReader` の基本的な使い方**
### **(1) ファイルの読み込み**
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedReaderExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
**ポイント:**
- `BufferedReader` を `FileReader` でラップすることで、ファイルからのデータ取得をバッファリング。
- `readLine()` を使って1行ずつ読み込み可能。
- `try-with-resources` を使用することで、ストリームを自動的にクローズ。

---

### **(2) 標準入力（コンソール）からの入力を受け取る**
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class ConsoleInputExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
            System.out.print("Enter your name: ");
            String name = br.readLine();
            System.out.println("Hello, " + name + "!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
**ポイント:**
- `System.in`（標準入力）を `InputStreamReader` でラップし、さらに `BufferedReader` でラップ。
- `readLine()` を使って一行の入力を取得。

---

## **3. `BufferedReader` の主なメソッド**
| メソッド           | 説明 |
|-------------------|----------------|
| `read()`         | 1文字（`char`）を読み込む。 |
| `readLine()`     | 1行を文字列として読み込む（`null` で終端）。 |
| `close()`        | ストリームを閉じる（`try-with-resources` を使うと自動クローズ）。 |
| `mark(int limit)` | 指定したバイト数までの位置をマーク（後で `reset()` で戻れる）。 |
| `reset()`        | `mark()` でマークした位置に戻る。 |
| `skip(long n)`   | 指定した文字数だけスキップする。 |

---

## **4. `BufferedReader` のメリット**
 **高速**（バッファリングにより、1文字ずつ読むよりもパフォーマンスが向上）  
 **メモリ効率が良い**（大量のデータを効率的に処理）  
 **便利なメソッド**（`readLine()` で簡単に1行ずつ取得可能）

---

## **5. `BufferedReader` vs `Scanner` の違い**
| 特徴 | `BufferedReader` | `Scanner` |
|------|----------------|------------|
| **速度** | 速い（バッファリングにより） | 遅い（パース処理があるため） |
| **用途** | テキストデータの読み込み向け | ユーザー入力や数値の解析向け |
| **メソッド** | `readLine()` で行単位で読み取り | `nextInt()`, `nextLine()` などでデータを解析 |

---

## **6. まとめ**
- **`BufferedReader` は、ファイルやコンソール入力を効率的に処理するためのクラス**。
- **バッファリングによってパフォーマンスを向上させる**。
- **`readLine()` を使って1行ずつデータを取得可能**。
- **`try-with-resources` を利用すると、安全にリソースを管理できる**。
