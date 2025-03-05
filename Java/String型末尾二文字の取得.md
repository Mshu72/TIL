Javaで`String`型の末尾から2文字を取得するには、`substring`メソッドを使用できます。

### **方法**
```java
public class Main {
    public static void main(String[] args) {
        String str = "HelloWorld";
        
        // 文字列の長さを取得
        int length = str.length();
        
        // 末尾から2文字を取得（長さが2以上の場合のみ）
        String lastTwoChars = length >= 2 ? str.substring(length - 2) : str;
        
        System.out.println(lastTwoChars); // 出力: ld
    }
}
```

---

### **解説**
1. `str.length()` で文字列の長さを取得。
2. `str.substring(length - 2)` で末尾2文字を取得。
   - `substring(startIndex)` の場合、指定したインデックスから末尾までを取得できます。
   - `length - 2` を開始位置とすれば、末尾2文字を取得できます。
3. `length >= 2` をチェックして、2文字未満のときはそのまま返すように処理。

---

### **注意点**
- 文字列の長さが2未満の場合、`substring(length - 2)` を直接使うと`StringIndexOutOfBoundsException`が発生するので、事前にチェックすると安全です。

---

### **補足: Optional を使う場合**
Java 8以降では、`Optional`を使って安全に処理する方法もあります。
```java
import java.util.Optional;

public class Main {
    public static void main(String[] args) {
        String str = "Hi";
        
        String result = Optional.ofNullable(str)
            .filter(s -> s.length() >= 2)
            .map(s -> s.substring(s.length() - 2))
            .orElse(str);
        
        System.out.println(result); // 出力: Hi
    }
}
```
この方法なら、`null` や短い文字列にも対応できます。
