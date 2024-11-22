`model` オブジェクトは、**Spring Framework** のアプリケーションで使用されるインターフェースで、**コントローラーからビューにデータを渡す役割**を果たします。具体的には、コントローラーで処理した結果をビューで表示したり、操作したりするために使用されます。

---

### **主な特徴**
1. **データの受け渡し**  
   - `model` オブジェクトにデータを追加することで、ビュー（Thymeleaf, JSP など）でそのデータを使用できます。
   - コントローラーからビューへデータを渡すための **"コンテナ"** と考えることができます。

2. **キーと値のペアでデータを保存**  
   - データはキー（名前）と値のペアとして保存されます。
   - キーを使ってビュー側で値にアクセスします。

3. **ビューで直接利用可能**  
   - `model.addAttribute("key", value)` としたデータは、ビュー内で `${key}` のように参照できます。

---

### **よく使われるメソッド**
以下は、`model` オブジェクトでよく使われるメソッドです：

#### **1. `addAttribute(String key, Object value)`**
   - キーと値をペアで追加します。
   - ビューでキーを使って値にアクセスできます。

   ```java
   model.addAttribute("message", "Hello, World!");
   ```

   **ビュー側（Thymeleafの例）**
   ```html
   <p>${message}</p> <!-- 結果: Hello, World! -->
   ```

#### **2. `addAllAttributes(Map<String, ?> attributes)`**
   - 複数の属性をまとめて追加します。
   - `Map` オブジェクトを渡し、その中のデータを一括でモデルに追加します。

   ```java
   Map<String, Object> data = new HashMap<>();
   data.put("name", "John");
   data.put("age", 30);
   model.addAllAttributes(data);
   ```

   **ビュー側**
   ```html
   <p>${name}, ${age}</p> <!-- 結果: John, 30 -->
   ```

#### **3. `containsAttribute(String key)`**
   - 指定したキーがモデル内に存在するか確認します。

   ```java
   if (model.containsAttribute("name")) {
       System.out.println("Name is present");
   }
   ```

#### **4. `asMap()`**
   - モデル内の全データを `Map` として取得します。

   ```java
   Map<String, Object> attributes = model.asMap();
   ```

---

### **`Model` と `ModelAndView` の違い**
- **`Model`**
  - データの受け渡しに特化したオブジェクト。
  - ビュー名はコントローラーのリターン値で指定します。

    ```java
    @GetMapping("/example")
    public String example(Model model) {
        model.addAttribute("message", "Hello, Model!");
        return "exampleView"; // ビュー名
    }
    ```

- **`ModelAndView`**
  - データ（Model）とビュー名の両方を設定できるオブジェクト。
  - 1つのオブジェクトでデータとビュー名を管理したい場合に便利です。

    ```java
    @GetMapping("/example")
    public ModelAndView example() {
        ModelAndView mav = new ModelAndView("exampleView");
        mav.addObject("message", "Hello, ModelAndView!");
        return mav;
    }
    ```

---

### **利用シーン**
- フォーム入力値を処理した結果をビューに返す場合：
  ```java
  @PostMapping("/submit")
  public String handleSubmit(@RequestParam String name, Model model) {
      model.addAttribute("greeting", "Hello, " + name + "!");
      return "result";
  }
  ```

  **ビュー側（Thymeleafの例）**
  ```html
  <p>${greeting}</p> <!-- 結果: Hello, [name]! -->
  ```

- コントローラーで作成したリストやマップをビューで表示する場合：
  ```java
  List<String> items = Arrays.asList("Item1", "Item2", "Item3");
  model.addAttribute("items", items);
  ```

  **ビュー側**
  ```html
  <ul>
      <li th:each="item : ${items}">[[${item}]]</li>
  </ul>
  ```

---

### **まとめ**
- `model` は、Spring MVCで **コントローラーからビューにデータを渡すためのオブジェクト** です。
- 主にキーと値のペアとしてデータを追加し、ビューで簡単に利用できます。
- シンプルなデータ渡しでは `Model` を、データとビュー名をまとめたい場合は `ModelAndView` を使い分けます。
