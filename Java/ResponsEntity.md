`ResponseEntity` は、Spring Boot において HTTP レスポンスをより柔軟に制御できるクラスです。  
通常の `@RestController` や `@ResponseBody` では、メソッドの戻り値が自動的に JSON 変換されてレスポンスとして返されますが、  
`ResponseEntity` を使用すると、HTTP ステータスコードやレスポンスヘッダーを明示的に設定できます。

---

## 基本的な使い方

### 1. **単純なレスポンス**
```java
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class SampleController {

    @GetMapping("/hello")
    public ResponseEntity<String> hello() {
        return ResponseEntity.ok("Hello, World!");
    }
}
```
**解説**:
- `ResponseEntity.ok("Hello, World!")` は、ステータスコード `200 OK` とともに `"Hello, World!"` を返します。

---

### 2. **ステータスコードを指定する**
```java
@GetMapping("/not-found")
public ResponseEntity<String> notFoundExample() {
    return ResponseEntity.status(404).body("Resource not found");
}
```
**解説**:
- `.status(404).body("Resource not found")` により、`404 Not Found` のレスポンスを返す。

---

### 3. **レスポンスヘッダーを追加する**
```java
import org.springframework.http.HttpHeaders;

@GetMapping("/custom-header")
public ResponseEntity<String> customHeaderExample() {
    HttpHeaders headers = new HttpHeaders();
    headers.add("X-Custom-Header", "CustomValue");
    return ResponseEntity.ok().headers(headers).body("With Custom Header");
}
```
**解説**:
- `HttpHeaders` を使って `X-Custom-Header` というカスタムヘッダーを追加。

---

### 4. **オブジェクトを JSON で返す**
```java
import org.springframework.http.HttpStatus;
import java.util.Map;

@GetMapping("/json")
public ResponseEntity<Map<String, Object>> jsonResponse() {
    Map<String, Object> response = Map.of(
        "message", "Success",
        "status", 200
    );
    return new ResponseEntity<>(response, HttpStatus.OK);
}
```
**解説**:
- `Map.of("message", "Success", "status", 200)` を JSON に変換して `200 OK` のレスポンスを返す。

---

### 5. **エラーハンドリングと `ResponseEntity`**
`ResponseEntity` は例外ハンドリングにも使えます。

#### **例: `@ExceptionHandler` を使う**
```java
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(RuntimeException.class)
    public ResponseEntity<String> handleRuntimeException(RuntimeException ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                             .body("Internal Server Error: " + ex.getMessage());
    }
}
```
**解説**:
- `RuntimeException` が発生した際に、`500 Internal Server Error` を返すカスタムエラーハンドリングを行う。

---

### **まとめ**
| メソッド | 説明 |
|----------|------|
| `ResponseEntity.ok(body)` | `200 OK` のレスポンスを返す |
| `ResponseEntity.status(HttpStatus.BAD_REQUEST).body(body)` | `400 Bad Request` など、カスタムステータスコードを指定 |
| `ResponseEntity.noContent().build()` | `204 No Content` を返す |
| `ResponseEntity.headers(headers).body(body)` | カスタムヘッダー付きのレスポンスを作成 |

---

### **`ResponseEntity` を使うメリット**
1. **ステータスコードを柔軟に制御** できる（200, 400, 500 など）。
2. **カスタムヘッダーを設定** できる。
3. **エラーハンドリングと組み合わせ** て使いやすい。

---

シンプルな API では `@ResponseBody` だけでも十分ですが、  
より細かく制御したい場合には `ResponseEntity` を活用すると便利になる。
