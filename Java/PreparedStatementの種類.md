**PreparedStatement**には種類やバリエーションがあります   
それは主に**利用方法**や**データベースドライバの特性**に基づいて分類されます。以下に、PreparedStatementの種類やその違いについて説明します。

---

### **1. 標準的なPreparedStatement**
- **概要**:
  - JDBC APIに標準で用意されている`PreparedStatement`。
  - SQL文を事前にコンパイルし、実行時にパラメータをバインドします。
- **特徴**:
  - 安全性（SQLインジェクション対策）とパフォーマンス向上が主目的。
- **利用例**:
  ```java
  String sql = "SELECT * FROM users WHERE id = ?";
  PreparedStatement pstmt = connection.prepareStatement(sql);
  pstmt.setInt(1, 123);
  ResultSet rs = pstmt.executeQuery();
  ```

---

### **2. Batch PreparedStatement（バッチ処理）**
- **概要**:
  - 一つのPreparedStatementで複数回のクエリをまとめて送信し、効率的に実行する仕組み。
  - 例えば、大量のデータを挿入する場合に有効。
- **特徴**:
  - ネットワーク負荷やデータベースへの接続回数を減らすことで、処理速度を向上。
  - トランザクションと組み合わせることで、データの整合性を確保可能。
- **利用例**:
  ```java
  String sql = "INSERT INTO users (name, email) VALUES (?, ?)";
  PreparedStatement pstmt = connection.prepareStatement(sql);

  pstmt.setString(1, "John");
  pstmt.setString(2, "john@example.com");
  pstmt.addBatch();

  pstmt.setString(1, "Jane");
  pstmt.setString(2, "jane@example.com");
  pstmt.addBatch();

  int[] result = pstmt.executeBatch(); // バッチ実行
  ```

---

### **3. CallableStatement（ストアドプロシージャ用）**
- **概要**:
  - ストアドプロシージャやストアドファンクションを呼び出すために使用。
  - `PreparedStatement` のサブインターフェースですが、ストアドプロシージャのパラメータや戻り値の取り扱いが特徴的。
- **特徴**:
  - ビジネスロジックをデータベース側に移譲する場合に利用。
  - IN/OUTパラメータを扱える。
- **利用例**:
  ```java
  String sql = "{CALL getUserById(?, ?)}"; // ストアドプロシージャ呼び出し
  CallableStatement cstmt = connection.prepareCall(sql);

  cstmt.setInt(1, 123); // INパラメータ
  cstmt.registerOutParameter(2, Types.VARCHAR); // OUTパラメータ

  cstmt.execute();

  String userName = cstmt.getString(2); // OUTパラメータの取得
  ```

---

### **4. Server-Side Prepared Statements（サーバサイド準備済みステートメント）**
- **概要**:
  - データベースサーバ側でステートメントのコンパイルや最適化を行う。
  - 一部のデータベース（例: PostgreSQL, MySQLなど）でサポート。
- **特徴**:
  - クエリの計画を再利用することで、クライアント-サーバ間の負荷を軽減。
  - 高頻度で同じクエリを実行する場合にパフォーマンスが向上。
- **注意点**:
  - データベースやドライバによっては、必ずしも有効ではない場合がある。

---

### **5. Named PreparedStatement（名前付きプレースホルダ）**
- **概要**:
  - 通常の`PreparedStatement`ではプレースホルダが`?`で指定されますが、名前付きプレースホルダを使用することで可読性が向上します。
  - 標準のJDBCには対応していませんが、ライブラリ（例: Hibernate, MyBatis）やフレームワークを利用することで可能。
- **特徴**:
  - 複雑なクエリで、どのパラメータがどの値に対応しているのかを明確にする。
- **利用例（MyBatisなど）**:
  ```sql
  SELECT * FROM users WHERE username = :username AND email = :email
  ```

---

### **6. PreparedStatementのオプション（JDBCの設定による分類）**
- **ResultSetのオプション指定**:
  - PreparedStatementを作成する際に、`ResultSet`のタイプや同時更新可能性を指定できます。
  - 例:
    ```java
    PreparedStatement pstmt = connection.prepareStatement(
        "SELECT * FROM users",
        ResultSet.TYPE_SCROLL_INSENSITIVE, // スクロール可能
        ResultSet.CONCUR_UPDATABLE         // 更新可能
    );
    ```

---

### **まとめ**
PreparedStatementには以下のようなバリエーションがあります:
1. 標準的なPreparedStatement（基本形）。
2. バッチ処理用のPreparedStatement。
3. ストアドプロシージャ用のCallableStatement。
4. サーバサイド準備済みステートメント（データベース依存）。
5. 名前付きPreparedStatement（ライブラリ依存）。
6. JDBC設定による特別なPreparedStatement。

**選択ポイント:**
- アプリケーションのニーズに応じて最適な種類を選択。
- データベースやJDBCドライバの機能を確認し、適切に使い分けることが重要です。
