オラクルDBにおける `MERGE` 文（別名「**アップサート（upsert）**」）は、**指定した条件で一致するレコードがあれば更新し、一致しなければ新しく挿入する**という、`INSERT` と `UPDATE` を1つにまとめた構文です。

---

## 基本構文

```sql
MERGE INTO 〈ターゲット表〉 target
USING 〈ソース表または副問い合わせ〉 source
ON (〈結合条件〉)
WHEN MATCHED THEN
    UPDATE SET 〈更新内容〉
WHEN NOT MATCHED THEN
    INSERT (〈列名1〉, 〈列名2〉, ...)
    VALUES (〈値1〉, 〈値2〉, ...);
```

---

## 各要素の意味

| 要素            | 説明 |
|----------------|------|
| `MERGE INTO`   | 更新対象（ターゲット）のテーブル |
| `USING`        | 比較するソーステーブルや副問い合わせ |
| `ON`           | 結合条件。一致すれば `UPDATE`、一致しなければ `INSERT` |
| `WHEN MATCHED` | 条件に一致した場合の更新処理 |
| `WHEN NOT MATCHED` | 条件に一致しなかった場合の挿入処理 |

---

## 使用例

### 例1: キー一致で更新、なければ挿入

```sql
MERGE INTO employees e
USING (
    SELECT 1001 AS emp_id, 'Taro' AS name, 'Sales' AS department FROM dual
) s
ON (e.emp_id = s.emp_id)
WHEN MATCHED THEN
    UPDATE SET e.name = s.name, e.department = s.department
WHEN NOT MATCHED THEN
    INSERT (emp_id, name, department)
    VALUES (s.emp_id, s.name, s.department);
```

このSQLは以下のように動作します：

- `employees` テーブルに `emp_id = 1001` の行があれば、`name` と `department` を更新。
- なければ、新しくレコードを挿入。

---

## よくある応用パターン

### 集計結果を別テーブルに反映

```sql
MERGE INTO sales_summary ss
USING (
  SELECT product_id, SUM(quantity) AS total_qty
  FROM sales
  GROUP BY product_id
) s
ON (ss.product_id = s.product_id)
WHEN MATCHED THEN
  UPDATE SET ss.total_qty = s.total_qty
WHEN NOT MATCHED THEN
  INSERT (product_id, total_qty)
  VALUES (s.product_id, s.total_qty);
```

---

## 注意点

- `ON` 条件が適切でないと、意図しない更新や重複挿入が発生することがあります。
- `USING` は `DUAL` を使えば単一レコードでアップサートが可能。
- `WHEN MATCHED THEN UPDATE` と `WHEN NOT MATCHED THEN INSERT` の **両方が省略不可**。片方だけ使う場合は、空のブロックを記述する必要があります。
- `MERGE` 文はトリガーや制約と絡む場合、制御に注意が必要。

