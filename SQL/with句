**`WITH`句**（Common Table Expression、CTE）とは、SQLで一時的な名前付き結果セット（テーブル）を定義し、それを後続のクエリで使用できる構文です。特に複雑なクエリを簡潔に記述したり、可読性を向上させたりする際に便利です。

---

### **特徴**
1. 一時的なビューとして扱う。
2. **再利用可能**：同じ計算やサブクエリを複数回書く必要がなくなる。
3. クエリを段階的に記述できる（複雑な処理を分割して記述）。
4. 多くのSQLデータベース（PostgreSQL、MySQL、Oracle、SQL Serverなど）でサポート。

---

### **基本構文**

```sql
WITH cte_name AS (
    -- クエリの定義
    SELECT ...
)
SELECT ...
FROM cte_name
WHERE ...;
```

---

### **例: 基本的な使い方**

#### 例1: 簡単なCTEの使用
以下は、社員情報から部署ごとの平均給与を求めるクエリです。

```sql
WITH DepartmentAverage AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM
        employees
    GROUP BY
        department_id
)
SELECT
    e.employee_id,
    e.department_id,
    e.salary,
    da.avg_salary
FROM
    employees e
    INNER JOIN DepartmentAverage da
    ON e.department_id = da.department_id
WHERE
    e.salary > da.avg_salary;
```

**処理の流れ:**
1. `WITH`句で`DepartmentAverage`というCTEを作成。
   - 部署ごとの平均給与を計算。
2. メインクエリで、このCTEを利用して「給与が平均を超える社員」を取得。

---

### **複数のCTEの定義**

複数の`WITH`句をカンマで区切って連続的に記述できます。

```sql
WITH
    CTE1 AS (
        SELECT ...
    ),
    CTE2 AS (
        SELECT ...
        FROM CTE1
    )
SELECT ...
FROM CTE2;
```

---

### **例2: CTEのネスト**
以下は、売上データから月ごとの売上合計を計算し、その結果を基に年間合計を求める例です。

```sql
WITH MonthlySales AS (
    SELECT
        month,
        SUM(sales) AS total_sales
    FROM
        sales_data
    GROUP BY
        month
),
AnnualSales AS (
    SELECT
        SUM(total_sales) AS total_annual_sales
    FROM
        MonthlySales
)
SELECT
    *
FROM
    AnnualSales;
```

---

### **再帰CTE**
`WITH`句は再帰的なクエリにも対応しており、階層データ（例: 親子関係を持つデータ）を処理するのに使用されます。

#### 例3: 再帰CTEの例（社員の管理階層を取得）

```sql
WITH RECURSIVE ManagementHierarchy AS (
    SELECT
        employee_id,
        manager_id,
        1 AS level
    FROM
        employees
    WHERE
        manager_id IS NULL -- トップのマネージャーを選択
    UNION ALL
    SELECT
        e.employee_id,
        e.manager_id,
        mh.level + 1
    FROM
        employees e
        INNER JOIN ManagementHierarchy mh
        ON e.manager_id = mh.employee_id
)
SELECT *
FROM ManagementHierarchy;
```

---

### **メリット**
1. **簡潔で分かりやすい**：複雑なクエリを分割して記述可能。
2. **再利用性**：同じサブクエリを何度も記述する必要がない。
3. **デバッグが容易**：各CTEを独立して確認できる。

---

### **注意点**
1. **パフォーマンス**：
   - 一部のデータベースでは`WITH`句が実行時にインラインサブクエリと同等に扱われるため、パフォーマンスに影響を与えることがあります。
   - 必要に応じてインデックスやヒントを考慮してください。
2. **データベースの対応**：
   - MySQLの場合、`WITH`句はバージョン8.0以降でサポート。

---
