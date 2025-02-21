Spring Bootにおける`void`メソッドの使い方は、**処理を実行することが目的で、呼び出し元に値を返す必要がない場合**に多用されます。特に、**コントローラーのエンドポイント、サービスクラス、イベントハンドラー、バッチ処理**などでよく使用されます。

---

##  **1. コントローラーでの `void` メソッド**
Spring MVCのコントローラーで、**レスポンスを直接制御する場合**に`void`メソッドを使います。

###  **例: レスポンスを直接操作する**
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@RestController
public class MyController {

    @GetMapping("/download")
    public void downloadFile(HttpServletResponse response) throws IOException {
        response.setContentType("text/plain");
        response.setHeader("Content-Disposition", "attachment; filename=\"example.txt\"");
        response.getWriter().write("Spring Bootでのファイルダウンロード例");
    }
}
```
- **ポイント**:  
  - `void`を使い、`HttpServletResponse`を通じてレスポンスをカスタム制御します。
  - `return`でオブジェクトを返すのではなく、**ストリーム操作やヘッダー設定**で直接レスポンスを処理。

---

##  **2. サービス層での `void` メソッド**
サービス層では、**データの保存や更新などの副作用を持つ処理**に`void`メソッドが適しています。

###  **例: データベースへの保存処理**
```java
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // 戻り値を必要としない保存処理
    public void saveUser(User user) {
        userRepository.save(user);
    }
}
```
- **ポイント**:  
  - `saveUser`は保存処理を行うだけで結果を返さない。
  - コントローラー側は成功/失敗をHTTPステータスで判断できます。

---

##  **3. スケジューリング処理での `void` メソッド**
Spring Bootでは、`@Scheduled`を使って定期実行タスクを作成する際に、`void`メソッドを使います。

###  **例: 定期バッチ処理**
```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class ScheduledTask {

    // 5秒ごとに実行されるタスク
    @Scheduled(fixedRate = 5000)
    public void reportCurrentTime() {
        System.out.println("現在時刻: " + System.currentTimeMillis());
    }
}
```
- **ポイント**:  
  - メソッドは何も返さず、処理だけを行います（ログ出力やデータ更新など）。
  - 戻り値が不要なため、`void`で十分。

---

##  **4. イベントハンドリングでの `void` メソッド**
Spring Bootでは、**アプリケーションイベント**を使って処理を非同期的に分離できます。`@EventListener`を使うメソッドも通常`void`型です。

###  **例: ユーザー登録イベントのハンドリング**
```java
import org.springframework.context.event.EventListener;
import org.springframework.stereotype.Component;

@Component
public class UserEventListener {

    @EventListener
    public void handleUserRegistered(UserRegisteredEvent event) {
        System.out.println("新しいユーザーが登録されました: " + event.getUsername());
    }
}
```
- **ポイント**:  
  - イベント処理が完了したことを通知する必要がないため`void`を使用。
  - イベント駆動アーキテクチャで**非同期的な処理**を行う際に有効。

---

##  **5. トランザクション処理における `void` メソッド**
トランザクション管理用のメソッドも、処理成功時に結果を返す必要がなければ`void`で記述します。

###  **例: トランザクション付き更新処理**
```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class OrderService {

    private final OrderRepository orderRepository;

    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }

    @Transactional
    public void processOrder(Long orderId) {
        Order order = orderRepository.findById(orderId)
            .orElseThrow(() -> new RuntimeException("注文が見つかりません"));
        order.setStatus("PROCESSED");
        orderRepository.save(order);
    }
}
```
- **ポイント**:  
  - `@Transactional`により、メソッド全体が**1つのトランザクション**として扱われます。
  - 結果を返す必要がないため、`void`を使用。

---

##  **6. REST APIでステータスコードのみを返す場合**
エンドポイントが**処理成功のステータスコードのみを返す場合**、`void`メソッドを使用します。

###  **例: 削除エンドポイント**
```java
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @DeleteMapping("/users/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)  // 204ステータスを返す
    public void deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
    }
}
```
- **ポイント**:  
  - 削除成功後、**204 No Content**を返すだけなので、戻り値を返す必要がない。
  - `@ResponseStatus`で適切なHTTPステータスを制御。

---

##  **まとめ: Spring Bootにおける `void` メソッドの使いどころ**

| 使用シーン                | 説明                                       | 例 |
|------------------------|------------------------------------------|---------------------------|
| **コントローラー**       | レスポンスを直接制御する場合                  | ファイルダウンロード処理     |
| **サービス層**           | 保存や削除などの副作用を伴う処理               | ユーザー登録、データ保存     |
| **スケジューラー**        | 定期実行処理などのバッチプロセス               | ログ出力、データ同期処理     |
| **イベントリスナー**       | イベント駆動型アーキテクチャのイベント処理        | 登録完了通知、メール送信     |
| **トランザクション処理**   | 成功時に結果を返す必要のないトランザクション制御   | 注文処理、在庫更新          |
| **REST API**           | 成功時ステータスコードのみ返す場合             | リソース削除 (204 No Content) |

---

###  **補足ポイント:**
- Spring Bootの世界では、**処理が成功したこと自体が「返すべき結果」であることも多いため、`void`メソッドが適切な選択肢**となります。
- **エラーハンドリング**は`@ExceptionHandler`や`@ControllerAdvice`で補完することで、`void`メソッドでも十分なエラーレスポンス設計が可能です。

