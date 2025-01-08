### **`COALESCE` 関数の解説 (Oracle SQL)**

`COALESCE`は、**複数の値の中から最初にNULLでない値を返す関数**です。  
もしすべての引数が`NULL`であれば、`NULL`を返します。

---

### **構文**
```sql
COALESCE(expr1, expr2, ..., exprN)
```

- **`expr1`〜`exprN`**：評価対象の式やカラム。最大で127個まで指定可能。  
- **戻り値**：最初に`NULL`でない値。すべて`NULL`の場合は`NULL`。

---

### **基本的な動作例**

#### 例1: 単純なCOALESCEの例
```sql
SELECT COALESCE(NULL, NULL, 'A', 'B') AS RESULT FROM DUAL;
```
**結果**：
```
RESULT
------
A
```
- 最初の2つの`NULL`はスキップされ、`'A'`が返されます。

#### 例2: すべてがNULLの場合
```sql
SELECT COALESCE(NULL, NULL, NULL) AS RESULT FROM DUAL;
```
**結果**：
```
RESULT
------
NULL
```

---

### **実用例**
#### 1. **NULLをデフォルト値に置き換える**
`NULL`の代わりに特定のデフォルト値を表示したい場合に使います。

```sql
SELECT 顧客名, COALESCE(電話番号, '未登録') AS 電話番号
FROM 顧客;
```
- 電話番号が`NULL`の顧客には「未登録」と表示されます。

---

#### 2. **複数の候補から最適な値を選ぶ**
```sql
SELECT 商品ID, COALESCE(価格_割引後, 価格_通常, 0) AS 価格
FROM 商品;
```
- 割引後価格があればそれを使用し、なければ通常価格を選択。どちらも`NULL`なら`0`を返します。

---

#### 3. **JOINでNULLを回避する**
`LEFT JOIN`などで結合条件が一致しない場合に`NULL`が出ることがあります。  
この場合、`COALESCE`で代替値を指定できます。

```sql
SELECT E.EQP_ID,
       COALESCE(P.POWER_SYMBOL, 'N/A') AS POWER_SYMBOL
FROM PWMG_EQPSTD E
LEFT JOIN PWMG_EQPPW_PKG P
    ON E.ID = P.ID;
```
- `PWMG_EQPPW_PKG`に`POWER_SYMBOL`が存在しない場合は「N/A」と表示されます。

---

### **COALESCEと`NVL`の違い**

| 機能                          | COALESCE                                      | NVL                          |
|-------------------------------|-----------------------------------------------|------------------------------|
| **引数の数**                   | 2つ以上 (最大127個)                            | 2つ                          |
| **評価順序**                   | 左から順に評価                                | 第一引数がNULLなら第二引数   |
| **戻り値のデータ型**           | 最初に`NULL`でない値のデータ型                 | 1番目の引数と同じデータ型    |
| **柔軟性**                     | より柔軟（複数の値を評価）                     | シンプル（2つの値だけ）       |
| **NULL以外がない場合の戻り値** | NULL                                          | NULL                         |

---

### **NVLとの使い分け**
- **簡単な2値判定**なら`NVL`  
- **3つ以上の候補**がある場合は`COALESCE`が便利です。

**例**：
```sql
-- NVL版
SELECT NVL(価格_割引後, 価格_通常) FROM 商品;

-- COALESCE版 (候補が3つ以上)
SELECT COALESCE(価格_特別割引, 価格_割引後, 価格_通常, 0) FROM 商品;
```

---

### **メリット**
- **複数のNULLチェックが簡潔に記述可能**。  
- **パフォーマンス**が良く、シンプルなコードでデータの整合性が保てます。

---

### **まとめ**
- `COALESCE`は**最初にNULLでない値を返す**便利な関数です。  
- **デフォルト値設定**や**NULL回避処理**で広く使われます。  
- `NVL`より柔軟性が高く、多くの候補から値を選ぶ処理に最適です。
