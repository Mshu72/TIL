`@NamedQuery` は、Java Persistence API（JPA）で用いられるアノテーションの1つで、JPQL（Java Persistence Query Language）を使った名前付きクエリを定義するために使用されます。

## 主な特徴
1. **名前付きクエリの定義**  
   クエリを事前に定義し、それに名前を付けておくことで、コードの中でクエリを簡単に呼び出すことができます。

2. **クエリの再利用性**  
   名前付きクエリを利用することで、同じJPQLクエリを複数箇所で再利用できます。

3. **パフォーマンスの向上**  
   名前付きクエリはアプリケーションが起動する際にコンパイルされ、データベースへの問い合わせが最適化されます。

---

## 使用例
### 名前付きクエリの定義

```java
import jakarta.persistence.Entity;
import jakarta.persistence.NamedQuery;

@Entity
@NamedQuery(
    name = "User.findByName",
    query = "SELECT u FROM User u WHERE u.name = :name"
)
public class User {
    @Id
    private Long id;
    private String name;
    private String email;

    // Getters and setters
}
```

上記の例では、`User` エンティティに対して `User.findByName` という名前付きクエリが定義されています。

### 名前付きクエリの使用

```java
import jakarta.persistence.EntityManager;
import jakarta.persistence.Persistence;
import jakarta.persistence.TypedQuery;

public class Main {
    public static void main(String[] args) {
        EntityManager em = Persistence.createEntityManagerFactory("my-persistence-unit").createEntityManager();
        em.getTransaction().begin();

        // 名前付きクエリの実行
        TypedQuery<User> query = em.createNamedQuery("User.findByName", User.class);
        query.setParameter("name", "Alice");
        User user = query.getSingleResult();

        System.out.println(user.getEmail());

        em.getTransaction().commit();
        em.close();
    }
}
```

ここでは、`em.createNamedQuery` メソッドを使って名前付きクエリを呼び出しています。

---

## メリット
1. **コードの分離**  
   JPQLクエリをエンティティクラスやコードから分離することで、コードの可読性を向上させます。

2. **変更が容易**  
   クエリの変更が必要な場合、名前付きクエリを一箇所変更するだけで済みます。

3. **クエリの検証**  
   アプリケーション起動時にクエリが検証されるため、間違ったクエリが実行時に発見されるのを防ぎます。

---

## 注意点
- **静的クエリのみ**  
  `@NamedQuery` は静的クエリを定義するために使用されるので、動的にクエリを生成したい場合には向きません。
  
- **複雑なクエリ**  
  非常に複雑なクエリを記述する場合は、クエリをメンテナンスしづらくなることがあります。

- **冗長性**  
  小規模なプロジェクトでは、シンプルなJPQLやクエリビルダー（例: `Criteria API`）を直接使った方が効率的な場合もあります。

---

## 複数の名前付きクエリの定義
エンティティに複数の名前付きクエリを定義する場合は、`@NamedQueries` を使います。

```java
import jakarta.persistence.Entity;
import jakarta.persistence.NamedQueries;
import jakarta.persistence.NamedQuery;

@Entity
@NamedQueries({
    @NamedQuery(name = "User.findByName", query = "SELECT u FROM User u WHERE u.name = :name"),
    @NamedQuery(name = "User.findAll", query = "SELECT u FROM User u")
})
public class User {
    @Id
    private Long id;
    private String name;
    private String email;

    // Getters and setters
}
```

---

名前付きクエリは、JPAを利用するプロジェクトでコードをクリーンに保ち、パフォーマンスを向上させるための有用なツールです。
