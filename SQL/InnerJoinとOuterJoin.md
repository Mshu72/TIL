`LEFT OUTER JOIN`と`INNER JOIN`の違いは、**結合結果にどの行を含めるか**にあります。

### 1. `INNER JOIN`の特徴
- **一致する行だけ**を結果に含めます。  
- 結合条件 (`ON`) に合致しない行は**結果から除外**されます。  
- 両方のテーブルで一致するデータが存在する場合にのみ、レコードが返されます。

**例**:
```sql
SELECT EQP.EQP_ID, PWR.POWER_SYMBOL
FROM PWMG_EQPSTD EQP
INNER JOIN PWMG_EQPPW_PKG PWR
    ON EQP.ID = PWR.ID;
```

**結果**:
- `PWMG_EQPSTD`と`PWMG_EQPPW_PKG`の`ID`が一致する行のみが返されます。  
- 一致しない`EQP.ID`があれば、その行は**完全に除外**されます。

---

### 2. `LEFT OUTER JOIN`の特徴
- **左側のテーブル (`FROM`句で指定したテーブル)** のすべての行が結果に含まれます。  
- 結合条件 (`ON`) に一致する行が右側のテーブルに存在しない場合は、右側のテーブルのカラムが`NULL`で補完されます。

**例**:
```sql
SELECT EQP.EQP_ID, PWR.POWER_SYMBOL
FROM PWMG_EQPSTD EQP
LEFT OUTER JOIN PWMG_EQPPW_PKG PWR
    ON EQP.ID = PWR.ID;
```

**結果**:
- `PWMG_EQPSTD`のすべての行が結果に含まれます。  
- `PWR.ID`が存在しない場合でも、`EQP.ID`に対応する行は残り、`PWR.POWER_SYMBOL`には`NULL`が入ります。

---

### 3. 違いの視覚的イメージ
```
PWMG_EQPSTD (左側のテーブル)
+---+------------+
| ID | EQP_NAME   |
+---+------------+
| 1  | EQP_A      |
| 2  | EQP_B      |
| 3  | EQP_C      |
| 4  | EQP_D      |
+---+------------+

PWMG_EQPPW_PKG (右側のテーブル)
+---+--------------+
| ID | POWER_SYMBOL|
+---+--------------+
| 1  | PWR_X       |
| 2  | PWR_Y       |
+---+--------------+

INNER JOINの結果:
+---+------------+--------------+
| ID | EQP_NAME   | POWER_SYMBOL |
+---+------------+--------------+
| 1  | EQP_A      | PWR_X        |
| 2  | EQP_B      | PWR_Y        |
+---+------------+--------------+

LEFT OUTER JOINの結果:
+---+------------+--------------+
| ID | EQP_NAME   | POWER_SYMBOL |
+---+------------+--------------+
| 1  | EQP_A      | PWR_X        |
| 2  | EQP_B      | PWR_Y        |
| 3  | EQP_C      | NULL         |
| 4  | EQP_D      | NULL         |
+---+------------+--------------+
```

---

### 4. どちらを使うべきか？
- **`INNER JOIN`を使うケース**  
  - 両方のテーブルに**関連するデータが存在する行だけ**が必要な場合。  
  - データの整合性を重視し、一致しないデータは不要な場合。

- **`LEFT OUTER JOIN`を使うケース**  
  - **左側のテーブルのすべての行**が必要な場合。  
  - 関連するデータが存在しない場合でも、基準となるデータは保持したい場合。  
  - NULLを返してもデータを欠損させたくない場合。

---

### 5. パフォーマンスの違い
- **`INNER JOIN`** は、`LEFT OUTER JOIN`より**高速**なことが多いです。  
  - 理由：`INNER JOIN`は一致する行だけを処理するため、結果セットが小さくなる傾向があるからです。  
- **`LEFT OUTER JOIN`** は結果セットが大きくなりやすく、不要な`NULL`行が多くなるとパフォーマンスに影響する可能性があります。  

---

### 6. 具体的なユースケース
- **`INNER JOIN`**  
  - 例: 注文がある顧客だけを表示  
    ```sql
    SELECT 顧客名, 注文ID
    FROM 顧客
    INNER JOIN 注文
    ON 顧客.ID = 注文.顧客ID;
    ```
  - **注文のない顧客は結果に表示されません。**

- **`LEFT OUTER JOIN`**  
  - 例: 注文の有無にかかわらず、すべての顧客を表示  
    ```sql
    SELECT 顧客名, 注文ID
    FROM 顧客
    LEFT OUTER JOIN 注文
    ON 顧客.ID = 注文.顧客ID;
    ```
  - **注文のない顧客は`注文ID`が`NULL`として表示されます。**

---

### 7. 結論
- `INNER JOIN`は「**一致するデータだけ**」、  
- `LEFT OUTER JOIN`は「**一致しない場合も左側のデータを保持**」。  
要件に応じて使い分けることが重要です。
