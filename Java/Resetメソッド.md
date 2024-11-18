Javaで`ResultSet`を操作する際には、データベースクエリの結果を処理するために使用します。以下は、主な`ResultSet`のメソッドとその使い方です。

---

### 主なメソッド一覧

1. **カーソル操作**
   - `boolean next()`: 次の行にカーソルを移動します。次の行が存在すれば`true`、存在しなければ`false`を返します。

2. **データ取得**
   - `String getString(String columnLabel)`: 指定した列の文字列データを取得します。
   - `int getInt(String columnLabel)`: 指定した列の整数データを取得します。
   - `double getDouble(String columnLabel)`: 指定した列の小数データを取得します。
   - `Date getDate(String columnLabel)`: 指定した列の`Date`データを取得します。
   - `Object getObject(String columnLabel)`: 列のデータを`Object`として取得します。
   - `String getString(int columnIndex)`: 列インデックスを指定してデータを取得します（1から始まるインデックス）。

3. **カーソル位置**
   - `boolean isBeforeFirst()`: カーソルが最初の行の前にあるか確認します。
   - `boolean isAfterLast()`: カーソルが最後の行の後にあるか確認します。
   - `boolean isFirst()`: 現在の行が最初の行か確認します。
   - `boolean isLast()`: 現在の行が最後の行か確認します。

4. **その他の操作**
   - `boolean wasNull()`: 直前の列値が`NULL`だったか確認します。
   - `void close()`: リソースを閉じます。

---

### `ResultSet`の使い方

以下は、基本的な`ResultSet`の操作例です。

```java
import java.sql.*;

public class ResultSetExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/your_database";
        String user = "your_username";
        String password = "your_password";

        String query = "SELECT id, name, age FROM users";

        try (Connection connection = DriverManager.getConnection(url, user, password);
             Statement statement = connection.createStatement();
             ResultSet resultSet = statement.executeQuery(query)) {

            // 結果セットをループ
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                int age = resultSet.getInt("age");

                System.out.println("ID: " + id + ", Name: " + name + ", Age: " + age);
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

### 注意点
1. **リソース管理**:
   - `ResultSet`を使い終わったら`close()`でリソースを解放します。`try-with-resources`を使うことで自動的に閉じることができます。
   
2. **データ型の対応**:
   - 列データ型に合ったメソッドを使用する必要があります。例外が発生する場合があります。

3. **NULL値の処理**:
   - データベースで`NULL`値を含む列を取得するときは`wasNull()`を使うと安全に判定できます。

---

質問や具体的なコード例が必要であれば教えてください！
