`@RequestBody` と `@RequestParam` は、Spring Boot のコントローラーでクライアントから送られたデータを受け取るためのアノテーションですが、それぞれの用途や違いについて詳しく解説します。

---

## 1. `@RequestBody`
`@RequestBody` は、**HTTP リクエストのボディ**（JSON や XML など）をオブジェクトにマッピングするために使用します。  
主に `POST`、`PUT`、`PATCH` などのリクエストで使用されます。

### **使い方**
```java
@RestController
@RequestMapping("/api")
public class UserController {

    @PostMapping("/users")
    public String createUser(@RequestBody User user) {
        return "User created: " + user.getName();
    }
}
```

### **リクエスト例**
```json
{
    "name": "Taro",
    "age": 30
}
```

### **特徴**
- リクエストボディ全体を Java オブジェクトとして受け取る
- JSON や XML のデータを `@RequestBody` 付きのパラメータに自動変換
- `Content-Type: application/json` などのリクエストヘッダーが必要
- クライアント側は `POST` や `PUT` などでデータを送信

---

## 2. `@RequestParam`
`@RequestParam` は、**URLのクエリパラメータまたはフォームデータ** を取得するために使用します。  
主に `GET` リクエストで使用されますが、`POST` でも `application/x-www-form-urlencoded` の場合に利用できます。

### **使い方**
```java
@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/users")
    public String getUser(@RequestParam String name, @RequestParam(required = false, defaultValue = "20") int age) {
        return "User: " + name + ", Age: " + age;
    }
}
```

### **リクエスト例**
#### **クエリパラメータで送る**
```
GET /api/users?name=Taro&age=30
```

#### **フォームデータで送る**
```
POST /api/users
Content-Type: application/x-www-form-urlencoded

name=Taro&age=30
```

### **特徴**
- URL の `?key=value` 形式で送られたデータを取得
- `required = false` を指定すると、省略可能にできる
- `defaultValue = "20"` のようにデフォルト値を設定可能
- フォームデータにも対応（`application/x-www-form-urlencoded`）

---

## 3. `@RequestBody` と `@RequestParam` の違いまとめ

| 項目 | `@RequestBody` | `@RequestParam` |
|------|--------------|--------------|
| データの取得元 | リクエストボディ（JSON, XML） | クエリパラメータ, フォームデータ |
| HTTP メソッド | `POST`, `PUT`, `PATCH` など | `GET`, `POST`（フォームデータ）|
| データ形式 | JSON, XML など | `key=value` 形式（クエリ, フォーム）|
| 変換方法 | Jackson などで Java オブジェクトに変換 | 文字列や基本型として取得 |
| `required` / `defaultValue` 設定 | 不可 | 可能 |

---

### **どちらを使うべきか？**
- **JSON や複雑なデータ構造を送る場合** → `@RequestBody`
- **シンプルなパラメータを送る場合** → `@RequestParam`

例えば、ユーザー情報の登録なら `@RequestBody` を使うのが適切ですが、検索条件のような簡単な値なら `@RequestParam` で十分です。

---

### **応用：両方を組み合わせる**
両方を組み合わせて使うことも可能です。

```java
@PostMapping("/users")
public String createUser(@RequestBody User user, @RequestParam String role) {
    return "User: " + user.getName() + " with role: " + role;
}
```
**リクエスト**
```
POST /api/users?role=admin
Content-Type: application/json

{
    "name": "Taro",
    "age": 30
}
```

このように、リクエストボディでデータを受け取りつつ、URL のパラメータで追加情報を渡すこともできます。

---

### **まとめ**
- `@RequestBody` は JSON/XML のリクエストボディをオブジェクトに変換
- `@RequestParam` は URL のクエリパラメータやフォームデータを取得
- どちらを使うかはリクエストのデータ形式によって決める
- 必要なら組み合わせて使うことも可能
