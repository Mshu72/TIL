SQLでは`SUBSTRING`関数を使うことで、文字列の一部を取得できます。

### 例:
#### **基本構文**
```sql
SUBSTRING(文字列, 開始位置, 取得する長さ)
```

### **使用例**
#### **1. 文字列から一部を取得**
```sql
SELECT SUBSTRING('Hello, World!', 8, 5);
```
**結果:** `World`

#### **2. 列データに対して使用**
```sql
SELECT SUBSTRING(name, 1, 3) AS short_name FROM users;
```
このSQLは、`users` テーブルの `name` 列の最初の3文字を取得します。

#### **3. `LEFT` や `RIGHT` を使った部分取得**
- **先頭からN文字取得**
```sql
SELECT LEFT(name, 3) FROM users;
```
- **末尾からN文字取得**
```sql
SELECT RIGHT(name, 3) FROM users;
```

#### **4. `POSITION` を使って動的に切り出し**
例えば、メールアドレスの`@`より後ろの部分を取得:
```sql
SELECT SUBSTRING(email FROM POSITION('@' IN email) + 1) FROM users;
```

#### **5. MySQLの`SUBSTRING_INDEX`**
MySQLでは、`SUBSTRING_INDEX`を使うと特定の文字で区切られた部分を取得できます。
```sql
SELECT SUBSTRING_INDEX('user@example.com', '@', -1);
```
**結果:** `example.com` （`@`の後ろの部分を取得）

---

### **まとめ**
SQLの`SUBSTRING`は、Javaの`substring`メソッドとほぼ同じ動作をします。  
また、`LEFT`や`RIGHT`、`POSITION`、`SUBSTRING_INDEX`(MySQL) などを組み合わせると、より柔軟な操作が可能です。
