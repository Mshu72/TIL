### **Oracle DB の CLOB 型について解説**

#### **1. CLOB（Character Large Object）とは？**
CLOB（Character Large Object）は、**大容量のテキストデータ**を格納するための Oracle Database のデータ型です。主に **長文のテキストデータ（レポート、ログ、XML、JSON など）** を扱う際に使用されます。

#### **2. CLOB の特徴**
- **最大サイズ**  
  最大 **4GB** までのデータを格納可能（Oracle 12c 以降は、`MAX_STRING_SIZE=EXTENDED` 設定時に 32TB まで可能）。
- **UNICODE 対応**  
  CLOB は **CHAR 型や VARCHAR2 型とは異なり、UNICODE** に対応しているため、多言語のデータも保存できる。
- **トランザクションサポート**  
  CLOB は **トランザクション管理の対象** であり、他のデータ型と同様に COMMIT や ROLLBACK が可能。
- **検索と更新の制限**  
  CLOB は通常の文字列型と比べて処理が重く、検索や更新の際に一部制約がある（`LIKE` 演算子の利用には `DBMS_LOB` パッケージが必要）。
- **LOB セグメントに格納**  
  CLOB データは通常、LOB セグメントに保存され、テーブルの行には LOB ロケータ（ポインタ）のみが格納される。

---

#### **3. CLOB の基本的な操作**
##### **(1) CLOB 型のカラムを持つテーブルの作成**
```sql
CREATE TABLE documents (
    id NUMBER PRIMARY KEY,
    content CLOB
);
```

##### **(2) CLOB データの挿入**
```sql
INSERT INTO documents (id, content) VALUES (1, 'これは長いテキストデータです...');
```

##### **(3) CLOB データの更新**
```sql
UPDATE documents SET content = '更新後のテキストデータ' WHERE id = 1;
```

##### **(4) CLOB データの取得**
```sql
SELECT content FROM documents WHERE id = 1;
```

---

#### **4. CLOB を操作する関数とパッケージ**
CLOB のデータは通常の `VARCHAR2` とは異なり、専用の関数や `DBMS_LOB` パッケージを利用して操作する必要があります。

##### **(1) CLOB の部分取得**
CLOB データが大きい場合、一部分だけ取得することも可能です。

```sql
SELECT DBMS_LOB.SUBSTR(content, 100, 1) FROM documents WHERE id = 1;
```
- `DBMS_LOB.SUBSTR(content, 100, 1)`  
  → CLOB の先頭から 100 バイト取得

##### **(2) CLOB の文字列連結**
CLOB 型のデータを連結する場合、`DBMS_LOB.APPEND` を利用する。

```sql
DECLARE
    v_clob CLOB;
BEGIN
    SELECT content INTO v_clob FROM documents WHERE id = 1;
    DBMS_LOB.APPEND(v_clob, ' 追加テキスト');
    UPDATE documents SET content = v_clob WHERE id = 1;
END;
```

##### **(3) CLOB の検索**
通常の `LIKE` では検索できないため、`DBMS_LOB.INSTR` を利用する。

```sql
SELECT id FROM documents WHERE DBMS_LOB.INSTR(content, '検索ワード') > 0;
```

---

#### **5. CLOB のパフォーマンス最適化**
CLOB は通常の `VARCHAR2` よりもパフォーマンスが低いため、以下の点に注意が必要です。

- **短いテキストなら VARCHAR2 を使う**  
  `VARCHAR2(4000)` で収まる場合、CLOB ではなく `VARCHAR2` を使用する方がパフォーマンスが向上。
- **インラインストレージの活用**  
  Oracle 12c 以降では `ENABLE STORAGE IN ROW` を指定すると、4000バイト以内のデータは行内に格納され、アクセスが速くなる。
  ```sql
  CREATE TABLE documents (
      id NUMBER PRIMARY KEY,
      content CLOB
  ) LOB (content) STORE AS (ENABLE STORAGE IN ROW);
  ```
- **CLOB インデックスの活用**  
  CLOB データを検索する場合、全文検索用の **Oracle Text** を活用すると高速化できる。
  ```sql
  CREATE INDEX doc_content_idx ON documents(content) INDEXTYPE IS CTXSYS.CONTEXT;
  ```

---

#### **6. CLOB の Java や PL/SQL での操作**
##### **(1) PL/SQL で CLOB を扱う**
```sql
DECLARE
    v_clob CLOB;
    v_text VARCHAR2(100);
BEGIN
    SELECT content INTO v_clob FROM documents WHERE id = 1;
    v_text := DBMS_LOB.SUBSTR(v_clob, 100, 1);
    DBMS_OUTPUT.PUT_LINE(v_text);
END;
```

##### **(2) Java で CLOB を扱う**
JDBC で CLOB を扱う場合は `Clob` クラスを利用。

```java
PreparedStatement pstmt = conn.prepareStatement("SELECT content FROM documents WHERE id = ?");
pstmt.setInt(1, 1);
ResultSet rs = pstmt.executeQuery();
if (rs.next()) {
    Clob clob = rs.getClob("content");
    String content = clob.getSubString(1, (int) clob.length());
    System.out.println(content);
}
```

---

### **7. CLOB のメリット・デメリット**
| 項目 | メリット | デメリット |
|------|---------|-----------|
| **データサイズ** | 4GB 以上のテキストデータを格納可能 | 通常の文字列よりも管理が複雑 |
| **UNICODE対応** | 多言語データを扱える | `VARCHAR2` よりも処理が重い |
| **トランザクション** | 一般的な `COMMIT` / `ROLLBACK` に対応 | 大量のデータを操作するとパフォーマンス低下 |
| **検索性能** | `Oracle Text` で全文検索が可能 | `LIKE` では直接検索不可（`DBMS_LOB.INSTR` を利用） |

---

### **8. まとめ**
- **CLOB は 4GB 以上のテキストデータを格納できるデータ型**
- **通常の VARCHAR2 とは異なり、LOB セグメントを利用して管理される**
- **検索や更新には `DBMS_LOB` パッケージの関数を活用する**
- **パフォーマンスチューニングのために、インラインストレージや Oracle Text を利用する**
- **大規模な CLOB 操作は PL/SQL や Java でのストリーミング処理が推奨**
