`@RequestParam` と `@PathVariable` は、Spring MVC で HTTP リクエストからデータを取得するために使用されますが、これらには明確な違いがあります。それぞれの役割と違いについて以下で解説します。

---

### **`@RequestParam`**
`@RequestParam` は、**クエリパラメータやフォームデータ**から値を取得するために使用されます。

#### 特徴
- URLの「クエリ文字列」部分（`?key=value`）から値を取得します。
- POSTリクエストの場合、`application/x-www-form-urlencoded`や`multipart/form-data`のデータから値を取得します。
- デフォルトで値が必須ですが、`required=false`を指定したり、`defaultValue`を設定することでオプションにできます。

#### 使用例

```java
@GetMapping("/user")
public String getUserByName(@RequestParam String name) {
    return "User name: " + name;
}
```

リクエスト:
```
GET /user?name=John
```

結果:
```
User name: John
```

---

### **`@PathVariable`**
`@PathVariable` は、**URLのパス部分**から値を取得するために使用されます。

#### 特徴
- URLの「パス」セグメント（スラッシュ`/`で区切られた部分）から値を取得します。
- 動的なURL構造に対応するために使用されます。
- リクエストマッピングで指定されたパスの一部と変数をマッピングします。

#### 使用例

```java
@GetMapping("/user/{id}")
public String getUserById(@PathVariable int id) {
    return "User ID: " + id;
}
```

リクエスト:
```
GET /user/123
```

結果:
```
User ID: 123
```

---

### **違いのまとめ**

| **項目**            | **`@RequestParam`**                          | **`@PathVariable`**                    |
|---------------------|---------------------------------------------|---------------------------------------|
| **取得場所**         | クエリパラメータやフォームデータ              | URLパス部分                            |
| **例**              | `GET /user?name=John`                      | `GET /user/123`                      |
| **用途**            | パラメータやオプション値を取得                | 動的なリソース識別子を取得            |
| **必要性の指定**     | `required`で必須/任意を指定可能               | 必須（パスに定義されていないとエラー）   |
| **複数パラメータ**   | 複数のクエリパラメータに対応可能               | 複数のパスセグメントに対応可能         |
| **値の形式**         | `?key=value` 形式                         | `/固定文字列/{変数}` 形式             |

---

### **実際の使用例を比較**

#### **1. `@RequestParam` の例**
リクエスト:
```
GET /search?query=Spring&sort=asc
```

コントローラー:
```java
@GetMapping("/search")
public String search(@RequestParam String query, @RequestParam String sort) {
    return "Query: " + query + ", Sort: " + sort;
}
```

結果:
```
Query: Spring, Sort: asc
```

#### **2. `@PathVariable` の例**
リクエスト:
```
GET /product/101
```

コントローラー:
```java
@GetMapping("/product/{id}")
public String getProduct(@PathVariable int id) {
    return "Product ID: " + id;
}
```

結果:
```
Product ID: 101
```

---

### **併用する場合**
`@RequestParam` と `@PathVariable` を同時に使用することも可能です。

リクエスト:
```
GET /order/1001?status=shipped
```

コントローラー:
```java
@GetMapping("/order/{id}")
public String getOrder(@PathVariable int id, @RequestParam String status) {
    return "Order ID: " + id + ", Status: " + status;
}
```

結果:
```
Order ID: 1001, Status: shipped
```

---

### **選択の基準**
- **`@PathVariable` を使用する場合**:
  - リソース（ユーザー、商品、注文など）を識別するための値がURLパスに含まれるとき。
  - 例: `/user/123`, `/product/456`.

- **`@RequestParam` を使用する場合**:
  - オプションのフィルタリングやソートなどの追加情報が必要なとき。
  - 例: `/search?query=spring`, `/list?sort=asc`.

---

`@RequestParam` と `@PathVariable` は用途が異なるため、適切なシチュエーションで使い分けることが重要です。  
