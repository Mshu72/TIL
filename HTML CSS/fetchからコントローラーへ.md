### **`fetch` を使って Java（Spring Boot）のコントローラにアクセスする方法**
`fetch` を利用して Spring Boot の REST API にアクセスする方法を解説します。

---

## **1. Spring Boot 側の設定**
### **① Spring Boot のコントローラを作成**
まず、Spring Boot のコントローラを作成し、`@RestController` を使ってエンドポイントを公開します。

#### **GETリクエストのハンドリング**
```java
@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/hello")
    public ResponseEntity<String> getHello() {
        return ResponseEntity.ok("Hello from Java!");
    }
}
```

#### **POSTリクエストのハンドリング**
```java
@RestController
@RequestMapping("/api")
public class MyController {

    @PostMapping("/data")
    public ResponseEntity<String> postData(@RequestBody Map<String, String> request) {
        String name = request.get("name");
        return ResponseEntity.ok("Received data: " + name);
    }
}
```

---

## **2. JavaScript の `fetch` を使ってアクセス**
### **① GETリクエスト**
```javascript
fetch("http://localhost:8080/api/hello")
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.text();
  })
  .then(data => console.log(data))  // "Hello from Java!" が表示される
  .catch(error => console.error("Fetch error:", error));
```

---

### **② POSTリクエスト**
```javascript
fetch("http://localhost:8080/api/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ name: "John Doe" })
})
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.text();
  })
  .then(data => console.log(data))  // "Received data: John Doe" が表示される
  .catch(error => console.error("Fetch error:", error));
```

---

## **3. CORS（クロスオリジン）の対応**
もしフロントエンドとバックエンドが異なるオリジン（例: `http://localhost:3000` から `http://localhost:8080` にリクエストする）場合、CORS（Cross-Origin Resource Sharing）の設定が必要になります。

### **Spring Boot 側で CORS を許可**
#### **方法 1: `@CrossOrigin` を使用**
```java
@CrossOrigin(origins = "http://localhost:3000")
@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/hello")
    public ResponseEntity<String> getHello() {
        return ResponseEntity.ok("Hello from Java!");
    }
}
```
`@CrossOrigin(origins = "http://localhost:3000")` をつけることで、特定のオリジンからのアクセスを許可できます。

#### **方法 2: グローバル設定を追加**
もし複数のエンドポイントでCORSを許可するなら、`WebMvcConfigurer` を使います。

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class CorsConfig {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                        .allowedOrigins("http://localhost:3000")
                        .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                        .allowedHeaders("*")
                        .allowCredentials(true);
            }
        };
    }
}
```

---

## **4. `fetch` を `async/await` で書く**
`fetch` は `async/await` を使うと、より可読性が高くなります。

```javascript
async function fetchData() {
  try {
    const response = await fetch("http://localhost:8080/api/hello");
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const data = await response.text();
    console.log(data); // "Hello from Java!"
  } catch (error) {
    console.error("Fetch error:", error);
  }
}

fetchData();
```

---

## **まとめ**
1. **GETリクエスト**
   - `fetch("http://localhost:8080/api/hello")`
2. **POSTリクエスト**
   - `fetch(url, { method: "POST", headers: {...}, body: JSON.stringify({...}) })`
3. **CORS の対応**
   - `@CrossOrigin` や `WebMvcConfigurer` を使う
4. **`async/await` で書くと可読性向上**

この方法を使えば、`fetch` を使って Java（Spring Boot）のコントローラと通信できます！ 🚀
