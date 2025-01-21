SQLの`UNION`は、複数のSELECT文の結果を1つに結合するための演算子です。主に、異なるクエリの結果を統合して一つの結果セットとして取得したい場合に使用します。



---

### 基本的な使い方
- **構文**：
  ```sql
  SELECT 列1, 列2, ...
  FROM テーブル1
  UNION
  SELECT 列1, 列2, ...
  FROM テーブル2;
  ```
- この場合、テーブル1とテーブル2のクエリ結果を結合します。

- **例**：
  ```sql
  SELECT name, age
  FROM employees
  WHERE department = 'HR'
  UNION
  SELECT name, age
  FROM contractors
  WHERE department = 'HR';
  ```
  - `employees`テーブルと`contractors`テーブルから「HR部門」に属する`name`と`age`のデータを結合して取得します。

---

### 特徴
1. **重複行の削除**：
   - `UNION`はデフォルトで重複した行を自動的に削除します。
   - もし、重複行を保持したい場合は、`UNION ALL`を使用します。

   ```sql
   SELECT name, age FROM employees
   UNION ALL
   SELECT name, age FROM contractors;
   ```

2. **列数とデータ型が一致している必要がある**：
   - `UNION`で結合するSELECT文は、**列の数**と**データ型**が一致している必要があります。
   - 列名はクエリの最初のSELECT文の列名が使われます。

   ```sql
   SELECT name, age FROM employees
   UNION
   SELECT name, hire_date FROM contractors; -- NG (データ型が異なる)
   ```

3. **並び順**：
   - 結果セット全体に対する`ORDER BY`句は、`UNION`の最後に指定します。
   ```sql
   SELECT name, age FROM employees
   UNION
   SELECT name, age FROM contractors
   ORDER BY name;
   ```

---

### 使用例と応用

1. **データを統合してレポートを作成**：
   - 例えば、複数の地域の売上データを統合して一つの結果セットにまとめる場合に使えます。
   ```sql
   SELECT region, sales
   FROM sales_north
   UNION
   SELECT region, sales
   FROM sales_south;
   ```

2. **異なるテーブルのデータを比較**：
   - `UNION`を使用して、2つのテーブルの共通部分を確認することも可能です。

3. **複数の条件での集約**：
   - 特定の条件に基づいたデータを複数クエリで抽出し、それらを統合することで複雑な分析が可能になります。

---

### `UNION`と`UNION ALL`の違い
| 特徴               | `UNION`                   | `UNION ALL`                  |
|--------------------|---------------------------|------------------------------|
| 重複行            | 自動的に削除する          | 重複行をそのまま保持する     |
| 処理速度          | やや遅い（重複削除があるため）| 速い（重複削除を行わない）   |
| 用途              | 重複を避けたい場合に使用  | 重複を許容する場合に使用     |

---

### 注意点
1. **パフォーマンス**：
   - 重複を削除する`UNION`は、特に大量のデータを処理する場合にパフォーマンスが低下することがあります。必要に応じて`UNION ALL`を使用することで速度を改善できます。

2. **NULLの扱い**：
   - `UNION`では`NULL`も重複行として扱われます。

3. **並び順の指定**：
   - 各SELECT文ごとに`ORDER BY`を指定することはできません。全体に対してのみ可能です。

---

`UNION`は、複数のクエリを統合する際に非常に便利ですが、注意点を押さえて効率的に使用することが重要です。用途に応じて`UNION`と`UNION ALL`を使い分けてください。
