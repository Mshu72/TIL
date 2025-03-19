`@Transactional(rollbackFor = Exception.class)` は、Spring Framework におけるトランザクション管理のためのアノテーションで、 **例外が発生した場合にトランザクションをロールバックする** ように指定するものです。

---

## **1. `@Transactional` の基本**
`@Transactional` は Spring が提供する **宣言型トランザクション管理** を行うためのアノテーションです。このアノテーションをメソッドやクラスに適用することで、メソッドの開始時にトランザクションを開始し、正常に終了したらコミット、例外が発生したらロールバックします。

```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class SampleService {

    @Transactional
    public void process() {
        // トランザクション開始
        // ここでデータベース操作 (INSERT, UPDATE, DELETE など) を行う
    } // 正常終了でコミット、例外発生でロールバック
}
```

---

## **2. `rollbackFor = Exception.class` の意味**
Spring のデフォルト動作では、 **`@Transactional` は `RuntimeException` (`unchecked exception`) が発生した場合にのみロールバック** します。

```java
@Transactional
public void process() throws Exception {
    throw new Exception("Checked Exception");  // デフォルトではロールバックされない
}
```

`Exception` は **`checked exception`** なので、このままではロールバックされません。

これを **明示的にロールバックさせるために** `rollbackFor = Exception.class` を指定します。

```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class SampleService {

    @Transactional(rollbackFor = Exception.class)
    public void process() throws Exception {
        // ここでデータベース操作を実行
        throw new Exception("例外発生！");  // rollbackFor があるのでロールバックされる
    }
}
```

### **つまり:**
 **デフォルト (`@Transactional` のみ)**
- `RuntimeException` (`NullPointerException`, `IllegalArgumentException` など) → **ロールバックされる**
- `Exception` (`IOException`, `SQLException` など) → **ロールバックされない**

 **`@Transactional(rollbackFor = Exception.class)`**
- `RuntimeException` → **ロールバック**
- `Exception` → **ロールバック**
- `Throwable` → **ロールバックされない**

---

## **3. `rollbackFor` のカスタマイズ**
`rollbackFor` には、 **特定の例外クラスを指定** することも可能です。

```java
@Transactional(rollbackFor = {SQLException.class, IOException.class})
public void process() throws SQLException, IOException {
    throw new SQLException("データベースエラー");  // ロールバック対象
}
```
→ `SQLException` や `IOException` のみロールバックし、それ以外の例外ではコミットされる。

---

## **4. `noRollbackFor` を使ったロールバックの制御**
`noRollbackFor` を指定すると、特定の例外だけ **ロールバックさせない** ことができます。

```java
@Transactional(rollbackFor = Exception.class, noRollbackFor = CustomException.class)
public void process() throws Exception {
    throw new CustomException("この例外ではロールバックしない");
}
```
→ `Exception` でロールバックされるが、 `CustomException` の場合はロールバックされない。

---

## **5. `rollbackFor = Throwable.class` を使うべきか？**
**`rollbackFor = Throwable.class` を指定すると、すべてのエラー（`Error`, `Exception`）がロールバック対象になります。**
しかし、`Error`（`OutOfMemoryError` や `StackOverflowError` など）は通常アプリケーションではハンドリングすべきではないため、 **`rollbackFor = Throwable.class` は通常推奨されません**。

```java
@Transactional(rollbackFor = Throwable.class)  // 推奨されない
public void process() throws Throwable {
    throw new OutOfMemoryError("システムエラー");
}
```

---

## **6. まとめ**
 `@Transactional` だけだと **`RuntimeException` のみロールバック対象**  
 `rollbackFor = Exception.class` を指定すると、 **`checked exception` でもロールバック**  
 `rollbackFor = {特定の例外.class}` でロールバック対象を限定できる  
 `noRollbackFor` で **特定の例外はロールバックしないようにできる**  
 `rollbackFor = Throwable.class` は、 **`Error` までロールバックしてしまうので注意**  
