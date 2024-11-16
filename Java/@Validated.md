`@Validated` アノテーションは、Spring Framework における入力データのバリデーション機能を有効化するために使用されます。主に以下の場面で利用されます。

---

## **1. 主な用途と特徴**
### **メソッドレベルのバリデーション**
`@Validated` を使用すると、メソッド引数に指定されたオブジェクトのバリデーションが実行されます。Spring が提供するバリデーションフレームワークを利用し、アノテーションを使った入力データの検証が可能です。

---

## **2. 具体的な使い方**

### **クラスレベルでの使用**
`@Validated` はクラスに付けることで、そのクラス内のメソッドのバリデーションを有効化します。

```java
import org.springframework.validation.annotation.Validated;

@Validated
public class SampleService {

    public void save(@Valid User user) {
        // バリデーション処理が自動的に実行される
    }
}
```

### **Controllerでの使用**
Spring MVC で、リクエストパラメータやボディの検証を行う際に使用されます。

```java
import org.springframework.web.bind.annotation.*;
import org.springframework.validation.annotation.Validated;

import javax.validation.Valid;

@RestController
@RequestMapping("/api")
@Validated
public class SampleController {

    @PostMapping("/users")
    public String createUser(@Valid @RequestBody User user) {
        return "User created";
    }
}
```

### **メソッドレベルのバリデーション (グループ指定)**
`@Validated` はグループ指定を伴うバリデーションにも使用されます。これは、異なる操作で異なる検証ルールを適用する場合に便利です。

```java
import org.springframework.validation.annotation.Validated;

@Validated(CreateGroup.class)
public class SampleService {

    public void createUser(@Valid User user) {
        // CreateGroup に基づいたバリデーションを実行
    }

    @Validated(UpdateGroup.class)
    public void updateUser(@Valid User user) {
        // UpdateGroup に基づいたバリデーションを実行
    }
}
```

---

## **3. `@Validated` と `@Valid` の違い**

| **アノテーション** | **用途**                                                                 |
|---------------------|---------------------------------------------------------------------------|
| `@Validated`       | Spring の提供する機能で、グループ化されたバリデーションなどが可能。          |
| `@Valid`           | JSR-303/JSR-380 (Bean Validation) のアノテーションで、標準的な検証を行う。 |

`@Validated` は Spring の拡張機能を利用できるため、グループ指定やカスタムバリデーションを実現する際に有用です。

---

## **4. 実行時の仕組み**

1. **対象オブジェクトの検証**: メソッドの引数に渡されたオブジェクトをチェック。
2. **検証エラーの管理**: 検証に失敗すると例外 (`ConstraintViolationException`) がスローされる。
3. **例外ハンドリング**: コントローラで適切に例外をキャッチしてエラーメッセージを返す。

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ConstraintViolationException.class)
    public ResponseEntity<String> handleValidationException(ConstraintViolationException e) {
        return ResponseEntity.badRequest().body("Validation error: " + e.getMessage());
    }
}
```

---

## **5. 注意点**

- **依存関係の追加**: Hibernate Validator などの Bean Validation プロバイダが必要です。
- **Spring Boot の設定**: Spring Boot では通常、`spring-boot-starter-validation` によって自動的にバリデーションが有効になります。
- **`@Valid` との併用**: 通常は引数レベルで `@Valid` を指定する必要があります。

---

`@Validated` を利用することで、入力データの安全性と正確性を保ちながら、グループバリデーションやカスタム検証ロジックを簡単に統合できます。
