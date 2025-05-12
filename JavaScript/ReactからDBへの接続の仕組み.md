React アプリは **フロントエンド**（ユーザー側）で動作するため、**直接データベースには接続しません**。
代わりに、**バックエンド（APIサーバー）を通して間接的にデータベースにアクセス**します。

---

## 全体の仕組み

```plaintext
[React (フロントエンド)]
     ⇅ HTTPリクエスト（fetch/axios）
[バックエンド（例：Node.js/Express, Spring Boot, Railsなど）]
     ⇅ SQLクエリまたはORM（Sequelize, Prisma, JPAなど）
[データベース（MySQL, PostgreSQL, MongoDBなど）]
```

---

## 構成要素の解説

### React（フロントエンド）

* `fetch()` や `axios` を使って、HTTP 経由でバックエンドにリクエストを送る。
* 例：

```javascript
useEffect(() => {
  fetch("http://localhost:3001/api/users")
    .then((res) => res.json())
    .then((data) => setUsers(data));
}, []);
```

---

### バックエンド（APIサーバー）

* React から受け取ったリクエストを処理し、データベースにアクセスする。
* 例：Node.js + Express の場合

```javascript
app.get("/api/users", async (req, res) => {
  const users = await db.query("SELECT * FROM users");
  res.json(users.rows);
});
```

---

### データベース

* SQL文やORM（Prisma, Sequelize, JPA など）を通じてデータを取得・保存する。
* バックエンドからのみ直接接続される。

---

## なぜ React から直接 DB にアクセスしないのか？

* **セキュリティ**：DB の認証情報や構造を外部に漏らさない。
* **構造の分離**：UIとデータ処理を分けることで保守性が上がる。
* **スケーラビリティ**：複数のフロントエンド（Web, モバイル）に共通の API を提供できる。

---

## まとめ

| 役割     | 内容                               |
| ------ | -------------------------------- |
| React  | ユーザー入力や画面表示、API呼び出し（fetch/axios） |
| バックエンド | API処理、DB接続、認証やバリデーションなど          |
| データベース | データ保存・取得、SQL実行                   |

---
