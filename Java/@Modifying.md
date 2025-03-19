### **`@Modifying` とは？**
`@Modifying` は、Spring Data JPA のアノテーションで、**データベースを変更する JPQL（またはネイティブ SQL）クエリを実行するメソッド** に付与します。

Spring Data JPA では、通常 `@Query` を使ってカスタムクエリを実行しますが、**`SELECT` 以外の `UPDATE`, `DELETE`, `INSERT` などの変更系クエリを実行する場合は `@Modifying` が必須** です。

---

## **1. `@Modifying` の基本的な使い方**
### **(1) `UPDATE` 文を使った例**
```java
import org.springframework.data.jpa.repository.Modifying;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {

    @Modifying
    @Transactional
    @Query("UPDATE User u SET u.name = :name WHERE u.id = :id")
    int updateUserName(@Param("id") Long id, @Param("name") String name);
}
```
 **ポイント**
- **`@Modifying` をつけると `UPDATE` や `DELETE` などの変更系クエリが実行可能**
- **`@Transactional` もセットで付ける**（変更系のクエリはトランザクション内で実行する必要がある）
- **返り値は `int` で、更新された行数を取得できる**

---

### **(2) `DELETE` 文を使った例**
```java
@Modifying
@Transactional
@Query("DELETE FROM User u WHERE u.id = :id")
int deleteUserById(@Param("id") Long id);
```
→ 指定した `id` のユーザーを削除する。

---

### **(3) `INSERT` は通常 `@Modifying` ではなく `save()` を使う**
JPA では、`INSERT` 文を直接使うよりも、`save()` メソッドでエンティティを作成するのが一般的。

```java
User user = new User();
user.setName("John Doe");
userRepository.save(user);
```
**ただし、ネイティブクエリを使う場合は `INSERT` も可能。**
```java
@Modifying
@Transactional
@Query(value = "INSERT INTO users (name, email) VALUES (:name, :email)", nativeQuery = true)
int insertUser(@Param("name") String name, @Param("email") String email);
```

---

## **2. `@Transactional` の重要性**
`@Modifying` を使うメソッドは、通常 `@Transactional` を **明示的に指定する必要がある**。

理由:
- `UPDATE` や `DELETE` は **データを変更するため、トランザクションが必要**
- もし `@Transactional` を指定しないと、**エラーになったり、トランザクションが適切に処理されないことがある**

---

## **3. `clearAutomatically = true` の使い方**
```java
@Modifying(clearAutomatically = true)
@Query("UPDATE User u SET u.active = false WHERE u.id = :id")
int deactivateUser(@Param("id") Long id);
```
 **`clearAutomatically = true` を指定すると、エンティティマネージャのキャッシュをクリア** する。

→ `UPDATE` や `DELETE` を実行した後、**エンティティマネージャのキャッシュに古いデータが残っている可能性があるため、クリアして最新のデータを取得するようにする。**

---

## **4. `flushAutomatically = true` の使い方**
```java
@Modifying(flushAutomatically = true)
@Query("UPDATE User u SET u.status = 'ACTIVE' WHERE u.id = :id")
int activateUser(@Param("id") Long id);
```
 **`flushAutomatically = true` を指定すると、実行前にエンティティマネージャの変更をフラッシュ（即時適用）する。**

→ `UPDATE` の前に未コミットの変更がある場合、それらを即座にデータベースに反映する。

---

## **5. `nativeQuery = true` でネイティブ SQL を実行**
```java
@Modifying
@Transactional
@Query(value = "UPDATE users SET email = :email WHERE id = :id", nativeQuery = true)
int updateEmail(@Param("id") Long id, @Param("email") String email);
```
 `nativeQuery = true` を指定すると、**JPQL ではなく純粋な SQL を実行可能。**

---

## **6. まとめ**
 **`@Modifying` は `UPDATE`, `DELETE`, `INSERT` などの変更系クエリで必須**  
 **`@Transactional` を併用しないとエラーが発生する可能性あり**  
 **変更がエンティティマネージャに反映されない場合、`clearAutomatically = true` を使う**  
 **ネイティブ SQL を実行する場合は `nativeQuery = true` を指定**  
 **返り値は影響を受けた行数 (`int`) になる**

JPA でデータを変更する際は、適切に `@Modifying` と `@Transactional` を使いましょう！
