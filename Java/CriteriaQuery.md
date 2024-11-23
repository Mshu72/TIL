### **CriteriaQuery とは**
`CriteriaQuery` は、Java Persistence API (JPA) が提供するプログラム的にクエリを構築するための API です。SQL のように文字列でクエリを書くのではなく、Java のオブジェクトを使ってクエリを動的に構築します。

動的クエリや複雑な条件のクエリをコード内で安全に構築できるのが利点です。

---

### **基本的な使い方**

`CriteriaQuery` を使用するには以下のステップが必要です。

1. **`EntityManager` の取得**  
   `EntityManager` は JPA の基本操作の入り口です。`CriteriaQuery` を作成するために必要です。

2. **`CriteriaBuilder` の取得**  
   `EntityManager` から `CriteriaBuilder` を取得し、クエリの部品（条件や式など）を構築します。

3. **`CriteriaQuery` の作成**  
   `CriteriaBuilder` を使ってクエリを生成します。クエリには対象エンティティ、フィルタ条件、並び替え、グループ化などを設定します。

4. **実行結果の取得**  
   `EntityManager` を使ってクエリを実行し、結果を取得します。

---

### **コード例: 基本的なクエリ**

以下は、JPA の `CriteriaQuery` を使用して、`BrBranch` エンティティのすべてのデータを取得する例です。

#### エンティティ
```java
@Entity
public class BrBranch {
    @Id
    private Long id;
    private String name;
    private Integer someValue;

    // ゲッターとセッター
}
```

#### `CriteriaQuery` を使用した全件取得
```java
@PersistenceContext
private EntityManager entityManager;

public List<BrBranch> getAllBranches() {
    // 1. CriteriaBuilder を取得
    CriteriaBuilder cb = entityManager.getCriteriaBuilder();

    // 2. CriteriaQuery を作成
    CriteriaQuery<BrBranch> query = cb.createQuery(BrBranch.class);

    // 3. ルートエンティティを指定
    Root<BrBranch> root = query.from(BrBranch.class);

    // 4. クエリの内容を指定（ここでは全件取得）
    query.select(root);

    // 5. クエリを実行して結果を取得
    return entityManager.createQuery(query).getResultList();
}
```

---

### **条件付きクエリ**

`CriteriaBuilder` を使用して条件（`WHERE` 句）を指定できます。

#### 条件付きクエリの例: `someValue > 10`
```java
public List<BrBranch> getBranchesWithSomeValueGreaterThan10() {
    CriteriaBuilder cb = entityManager.getCriteriaBuilder();
    CriteriaQuery<BrBranch> query = cb.createQuery(BrBranch.class);
    Root<BrBranch> root = query.from(BrBranch.class);

    // 条件を指定
    query.select(root)
         .where(cb.gt(root.get("someValue"), 10)); // someValue > 10

    return entityManager.createQuery(query).getResultList();
}
```

---

### **集計クエリ**

`CriteriaBuilder` を使用すると、`MAX`, `MIN`, `AVG`, `COUNT` などの集計関数を利用できます。

#### 最大値を取得するクエリの例
```java
public Integer getMaxSomeValue() {
    CriteriaBuilder cb = entityManager.getCriteriaBuilder();
    CriteriaQuery<Integer> query = cb.createQuery(Integer.class);
    Root<BrBranch> root = query.from(BrBranch.class);

    // 最大値を指定
    query.select(cb.max(root.get("someValue")));

    return entityManager.createQuery(query).getSingleResult();
}
```

---

### **並び替え**

クエリに `ORDER BY` を追加するには、`CriteriaQuery.orderBy` メソッドを使用します。

#### 並び替えの例: `name` を昇順でソート
```java
public List<BrBranch> getAllBranchesSortedByName() {
    CriteriaBuilder cb = entityManager.getCriteriaBuilder();
    CriteriaQuery<BrBranch> query = cb.createQuery(BrBranch.class);
    Root<BrBranch> root = query.from(BrBranch.class);

    // 並び替えを指定
    query.select(root)
         .orderBy(cb.asc(root.get("name"))); // name ASC

    return entityManager.createQuery(query).getResultList();
}
```

---

### **複数条件のクエリ**

`CriteriaBuilder` を使用して複数の条件を組み合わせることができます。

#### 条件の組み合わせ例: `someValue > 10 AND name LIKE '%Branch%'`
```java
public List<BrBranch> getFilteredBranches() {
    CriteriaBuilder cb = entityManager.getCriteriaBuilder();
    CriteriaQuery<BrBranch> query = cb.createQuery(BrBranch.class);
    Root<BrBranch> root = query.from(BrBranch.class);

    // 複数の条件を指定
    Predicate condition1 = cb.gt(root.get("someValue"), 10); // someValue > 10
    Predicate condition2 = cb.like(root.get("name"), "%Branch%"); // name LIKE '%Branch%'

    query.select(root)
         .where(cb.and(condition1, condition2)); // AND 条件

    return entityManager.createQuery(query).getResultList();
}
```

---

### **グループ化と集計**

グループ化（`GROUP BY`）と集計を組み合わせることもできます。

#### グループ化の例: `COUNT` と `GROUP BY`
```java
public List<Object[]> getBranchCountGroupedBySomeValue() {
    CriteriaBuilder cb = entityManager.getCriteriaBuilder();
    CriteriaQuery<Object[]> query = cb.createQuery(Object[].class);
    Root<BrBranch> root = query.from(BrBranch.class);

    // GROUP BY と集計
    query.multiselect(root.get("someValue"), cb.count(root))
         .groupBy(root.get("someValue"));

    return entityManager.createQuery(query).getResultList();
}
```

---

### **メリット**
1. **動的クエリ**: クエリをプログラム的に動的に構築できます。
2. **安全性**: クエリを直接文字列で書かないため、SQL インジェクションのリスクが減少します。
3. **複雑な条件に対応**: 複数の条件や集計を簡潔に組み込めます。

### **デメリット**
1. **冗長性**: 簡単なクエリでもコードがやや長くなりがちです。

