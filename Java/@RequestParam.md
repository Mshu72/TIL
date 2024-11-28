`@RequestParam` は、Spring FrameworkにおいてHTTPリクエストからパラメータを取得するために使用されるアノテーションです。特に、クエリパラメータやフォームデータをコントローラーのメソッドにマッピングする際に役立ちます。


---

### 基本的な使い方

HTTPリクエストのURLに含まれるパラメータを取得します。  
例えば、次のようなURLがリクエストされたとします。

```
GET /greet?name=John
```

これを処理するコントローラーメソッドは以下のように記述できます。

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    @GetMapping("/greet")
    public String greet(@RequestParam String name) {
        return "Hello, " + name + "!";
    }
}
```

上記のコードでは、`name`というクエリパラメータが`@RequestParam`を通じてメソッド引数に渡されます。この例では`name`が必須であるため、リクエストに含まれないとエラーが発生します。

---

### オプションのパラメータ

必須ではないパラメータの場合は、`required`属性を使用します。

```java
@GetMapping("/greet")
public String greet(@RequestParam(required = false, defaultValue = "Guest") String name) {
    return "Hello, " + name + "!";
}
```

- `required = false`：パラメータがなくてもエラーになりません。
- `defaultValue = "Guest"`：パラメータが指定されなかった場合のデフォルト値を設定します。

この例では、`/greet`だけをリクエストした場合に `"Hello, Guest!"` が返されます。

---

### 複数のパラメータ

複数のクエリパラメータを処理する場合は、それぞれに`@RequestParam`を付けます。

```java
@GetMapping("/sum")
public int sum(@RequestParam int a, @RequestParam int b) {
    return a + b;
}
```

例えば、`/sum?a=5&b=3` のリクエストに対して、結果は `8` となります。

---

### Mapでパラメータを取得

すべてのクエリパラメータを一括で取得したい場合は、`Map`を利用できます。

```java
@GetMapping("/params")
public String getParams(@RequestParam Map<String, String> params) {
    return "Parameters are: " + params.toString();
}
```

例えば、`/params?key1=value1&key2=value2` というリクエストが送られると、`params`は`{"key1":"value1", "key2":"value2"}`となります。

---

### パラメータの型変換

`@RequestParam`はリクエストパラメータを自動的に適切な型に変換します。例えば、`int`や`double`などのプリミティブ型や、カスタムの型コンバーターを設定して複雑な型をサポートすることもできます。

```java
@GetMapping("/convert")
public String convert(@RequestParam int number) {
    return "Number is: " + number;
}
```

クエリパラメータが数値でない場合は、400 Bad Requestエラーが発生します。

---

### 注意点

1. **リクエストパラメータが必須でエラーになる場合**：
   `@RequestParam`で`required=true`（デフォルト）に設定されたパラメータが不足すると、`400 Bad Request`エラーが発生します。

2. **デフォルト値の活用**：
   パラメータがオプションの場合、`defaultValue`を設定すると安全に処理できます。

3. **大規模なパラメータの処理**：
   Mapやカスタムオブジェクトを利用すると、複数のパラメータを効率的に処理できます。

---

