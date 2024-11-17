`@RestController` は、Spring Framework において RESTful Web サービスを構築する際に使用されるアノテーションです。`@Controller` と `@ResponseBody` の組み合わせを簡略化したもので、主に API を提供するコントローラーに適しています。

---

### 主なポイント

#### 1. **`@RestController`の役割**
`@RestController` は、クラスを REST API のエンドポイントとして機能させます。このアノテーションをクラスに付けることで、以下のことが自動的に行われます：

- そのクラス内のすべてのメソッドの戻り値は、デフォルトで HTTP レスポンスのボディに書き込まれる。
- 各メソッドが直接データ（JSON または XML 形式など）を返すために適している。

---

#### 2. **`@Controller` との違い**
| 特徴                   | @Controller                     | @RestController               |
|------------------------|----------------------------------|--------------------------------|
| **戻り値の扱い**        | ビュー名を返す（HTML など）       | データを直接返す（JSON など）  |
| **レスポンスボディ**    | 必要に応じて`@ResponseBody`を付加 | デフォルトでレスポンスボディに |

例えば、`@RestController` を使わない場合は、以下のように記述します：

```java
@Controller
@ResponseBody
public class MyController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

これを `@RestController` を使うと簡略化できます：

```java
@RestController
public class MyController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

---

#### 3. **典型的な使い方**
以下は、`@RestController` を用いた簡単な例です。

```java
@RestController
@RequestMapping("/api")
public class MyApiController {

    @GetMapping("/greet")
    public String greet() {
        return "Hello, API!";
    }

    @PostMapping("/add")
    public Map<String, String> add(@RequestBody Map<String, String> request) {
        // リクエストボディを受け取り、JSON 形式でレスポンスを返す
        Map<String, String> response = new HashMap<>();
        response.put("message", "Data received!");
        response.put("data", request.get("data"));
        return response;
    }
}
```

---

#### 4. **主な利点**
- **シンプル**: デフォルトでレスポンスボディが JSON にシリアライズされるため、コードが簡潔になる。
- **REST APIに特化**: RESTful サービス構築に最適。
- **拡張性**: 必要に応じて `@ExceptionHandler` や `ResponseEntity` を使ってカスタマイズが可能。

---

#### 5. **注意点**
- ビューを返したい場合には `@RestController` は適さない（その場合は `@Controller` を使う）。
- RESTful サービスの開発では通常、`@RequestMapping` やその派生（`@GetMapping`, `@PostMapping` など）と組み合わせて使う。

---

`@RestController` は、Spring Boot を使ってモダンな RESTful API を簡単に構築するための便利なアノテーションです。エンドポイントの実装に際して、特にフロントエンドとの JSON 形式でのデータのやり取りが必要な場合に役立ちます。
