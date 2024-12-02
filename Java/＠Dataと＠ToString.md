Oracle Database で `DATE` 型データを入力するには、以下の方法を使用します。

---

### **1. 文字列を `DATE` 型に変換して入力**
Oracle の `DATE` 型は、年月日 (YYYY-MM-DD) だけでなく、時分秒 (HH24:MI:SS) も含むデータ型です。そのため、適切なフォーマットを指定して入力します。

#### **`TO_DATE` 関数を使用**
- `TO_DATE` 関数で文字列を `DATE` 型に変換します。
- フォーマットを指定することで、文字列を正しく変換できます。

```sql
INSERT INTO your_table (date_column)
VALUES (TO_DATE('2024-12-02', 'YYYY-MM-DD'));
```

#### **時分秒を含む場合**
```sql
INSERT INTO your_table (date_column)
VALUES (TO_DATE('2024-12-02 14:30:00', 'YYYY-MM-DD HH24:MI:SS'));
```

---

### **2. `SYSDATE` を使用**
現在の日時を `DATE` 型で入力したい場合は、Oracle の組み込み関数 `SYSDATE` を使います。

```sql
INSERT INTO your_table (date_column)
VALUES (SYSDATE);
```

`SYSDATE` は現在の日時 (年月日と時分秒) を返します。

---

### **3. SQL 標準の日付リテラルを使用**
SQL 標準形式の日付リテラルも使用できます。この場合は固定のフォーマットで指定します。

#### **日付だけを指定**
```sql
INSERT INTO your_table (date_column)
VALUES (DATE '2024-12-02');
```

#### **日時を指定**
```sql
INSERT INTO your_table (date_column)
VALUES (TIMESTAMP '2024-12-02 14:30:00');
```

---

### **4. デフォルトフォーマットに依存する入力**
Oracle の `NLS_DATE_FORMAT` パラメータで定義されたデフォルトフォーマットに従えば、文字列を直接入力できます。

#### **現在の `NLS_DATE_FORMAT` を確認**
```sql
SELECT VALUE 
FROM NLS_SESSION_PARAMETERS 
WHERE PARAMETER = 'NLS_DATE_FORMAT';
```

デフォルトフォーマットが `DD-MON-YYYY` の場合：
```sql
INSERT INTO your_table (date_column)
VALUES ('02-DEC-2024');
```

> **注意:** デフォルトフォーマットが変更されると、この方法はエラーの原因となる可能性があるため、明示的に `TO_DATE` を使用する方が推奨されます。

---

### **5. バインド変数を使用**
アプリケーションから SQL を実行する場合は、バインド変数に `java.sql.Date` などを使って直接値を渡します。

例 (Java):
```java
PreparedStatement pstmt = connection.prepareStatement("INSERT INTO your_table (date_column) VALUES (?)");
pstmt.setDate(1, java.sql.Date.valueOf("2024-12-02"));
pstmt.executeUpdate();
```

---

### **まとめ**
- 明示的に `TO_DATE` を使うと安全で柔軟。
- 現在日時なら `SYSDATE`。
- SQL 標準の日付リテラルはシンプルで確実。
- アプリケーション側から操作する場合はバインド変数を利用。
