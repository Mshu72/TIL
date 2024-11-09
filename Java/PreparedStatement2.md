### **PreparedStatementについて**

`PreparedStatement` は、JavaのJDBC（Java Database Connectivity）APIで用いられるインターフェースの一つで、データベースとの安全かつ効率的なやり取りを可能にします。

#### **主な特徴**
1. **SQLインジェクション対策**
   - `PreparedStatement` は、SQLクエリのプレースホルダ（`?`）にパラメータをバインドする仕組みを提供します。
   - ユーザー入力を文字列としてエスケープ処理し、安全にクエリを実行することで、SQLインジェクション攻撃を防ぎます。

2. **パフォーマンス向上**
   - クエリが事前にコンパイルされ、同じクエリを複数回実行する場合に効率的です。
   - データベースは、毎回SQL文を解析する必要がなくなり、パフォーマンスが向上します。

3. **コードの可読性向上**
   - パラメータを動的に設定できるため、複雑なSQL文でもコードが読みやすくなります。

---

#### **基本的な使用方法**
以下は、`PreparedStatement` の基本的な流れを示します。

```java
import java.sql.*;

public class PreparedStatementExample {
    public static void main(String[] args) {
        // データベース接続情報
        String url = "jdbc:mysql://localhost:3306/your_database";
        String user = "your_username";
        String password = "your_password";

        // SQL文（プレースホルダ付き）
        String sql = "SELECT * FROM users WHERE username = ? AND password = ?";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            // PreparedStatementの作成
            PreparedStatement pstmt = conn.prepareStatement(sql);

            // パラメータをバインド
            pstmt.setString(1, "testUser");  // 1番目の`?`に値をセット
            pstmt.setString(2, "testPassword");  // 2番目の`?`に値をセット

            // クエリを実行
            ResultSet rs = pstmt.executeQuery();

            // 結果の処理
            while (rs.next()) {
                System.out.println("User ID: " + rs.getInt("id"));
                System.out.println("Username: " + rs.getString("username"));
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

#### **PreparedStatementのメソッド**
- **`setXxx` メソッド**
  - パラメータを設定するためのメソッド。
  - 例:
    - `setString(int parameterIndex, String value)`  
    - `setInt(int parameterIndex, int value)`
    - `setDate(int parameterIndex, java.sql.Date value)`
  
- **`execute` 系メソッド**
  - `executeQuery()`:
    - データを取得するクエリ（`SELECT` 文）で使用。
  - `executeUpdate()`:
    - データを変更するクエリ（`INSERT`、`UPDATE`、`DELETE` 文）で使用。
  - `execute()`:
    - 汎用的な実行メソッド。

---

#### **トランザクション管理とPreparedStatement**
`PreparedStatement` は、トランザクション制御と組み合わせて利用することが多いです。

```java
try (Connection conn = DriverManager.getConnection(url, user, password)) {
    conn.setAutoCommit(false); // トランザクションを開始

    String insertSQL = "INSERT INTO orders (product_id, quantity) VALUES (?, ?)";
    try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
        pstmt.setInt(1, 101);
        pstmt.setInt(2, 3);
        pstmt.executeUpdate();

        conn.commit(); // 成功時にコミット
    } catch (SQLException e) {
        conn.rollback(); // エラー時にロールバック
        e.printStackTrace();
    }
}
```

---

#### **まとめ**
- **安全性**: SQLインジェクションを防止。
- **効率性**: クエリの再利用でパフォーマンス向上。
- **可読性**: パラメータの動的バインディングでコードが明確。

`PreparedStatement` を使うことで、安全で効率的なデータベース操作が可能となります。
