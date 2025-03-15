# **Pandasライブラリの解説**  

Pandas（パンダス）は、Python の **データ分析** や **データ操作** に特化したライブラリです。  
Excel や SQL のようにデータを扱うことができ、特に **データフレーム（DataFrame）** という形式での操作が得意です。

---

## **1. Pandas の特徴**
 **データの読み書き**（CSV, Excel, SQL, JSON など）  
 **データのフィルタリング・集計**（Excel のピボットテーブルのような操作）  
 **欠損値処理**（NaN を埋める、削除する）  
 **データの可視化**（Matplotlib や Seaborn と組み合わせて使用）  
 **高速な計算**（NumPy を内部で使用しており、処理が速い）  

---

## **2. Pandas の基本データ構造**
Pandas には、主に **2つのデータ構造** があります。

### **① Series（1次元データ：リストや辞書のようなもの）**
```python
import pandas as pd

data = pd.Series([10, 20, 30, 40])
print(data)
```
 **出力結果**
```
0    10
1    20
2    30
3    40
dtype: int64
```
- **Series** は **インデックス付きのリスト** のようなもの
- **辞書のキーのようにインデックスを指定してアクセス可能**
  ```python
  print(data[1])  # 20
  ```

---

### **② DataFrame（2次元データ：Excel の表のようなもの）**
```python
df = pd.DataFrame({
    '名前': ['太郎', '花子', '次郎'],
    '年齢': [25, 30, 22],
    '職業': ['エンジニア', 'デザイナー', '教師']
})
print(df)
```
 **出力結果**
```
    名前  年齢     職業
0  太郎  25  エンジニア
1  花子  30  デザイナー
2  次郎  22    教師
```
- **DataFrame** は **行と列を持つデータ構造** で、**Excel や SQL のテーブルのようなもの**
- **列名を指定してデータにアクセスできる**
  ```python
  print(df['名前'])  # 名前の列を取得
  ```

---

## **3. Pandas の基本操作**
### **① CSVファイルの読み書き**
```python
# CSVファイルを読み込む
df = pd.read_csv("data.csv")

# CSVファイルに書き出す
df.to_csv("output.csv", index=False)
```
- `pd.read_csv("ファイル名")` → **CSV を DataFrame に変換**
- `df.to_csv("ファイル名")` → **DataFrame を CSV に保存**

---

### **② データの確認**
```python
print(df.head())  # 最初の5行を表示
print(df.tail())  # 最後の5行を表示
print(df.info())  # データの概要を表示
print(df.describe())  # 数値データの統計情報を表示
```
- `head()` → **最初の数行を表示**
- `tail()` → **最後の数行を表示**
- `info()` → **データ型や欠損値の確認**
- `describe()` → **平均値、標準偏差などの統計情報を取得**

---

### **③ データのフィルタリング**
```python
# 年齢が25以上のデータを抽出
df_filtered = df[df['年齢'] >= 25]
print(df_filtered)
```
 **出力結果**
```
    名前  年齢      職業
0  太郎  25  エンジニア
1  花子  30  デザイナー
```
- **条件を指定してデータを抽出** できる（SQL の `WHERE` のような操作）

---

### **④ データのグループ化（集計）**
```python
# 職業ごとの平均年齢を計算
df_grouped = df.groupby('職業')['年齢'].mean()
print(df_grouped)
```
**出力結果**
```
職業
エンジニア    25.0
デザイナー    30.0
教師        22.0
Name: 年齢, dtype: float64
```
- `groupby()` を使って **データをグループ化し、平均や合計を計算** できる

---

## **4. 欠損値処理（NaN の処理）**
```python
# 欠損値（NaN）があるデータフレーム
df = pd.DataFrame({
    '名前': ['太郎', '花子', None],
    '年齢': [25, None, 22],
    '職業': ['エンジニア', 'デザイナー', '教師']
})

# 欠損値を削除
df_cleaned = df.dropna()

# 欠損値を特定の値で埋める
df_filled = df.fillna({'名前': '不明', '年齢': 0})

print(df_cleaned)
print(df_filled)
```
- `dropna()` → **欠損値のある行を削除**
- `fillna()` → **欠損値を特定の値で埋める**

---

## **5. データの可視化**
Pandas は **Matplotlib** や **Seaborn** と連携してデータを簡単に可視化できます。

```python
import matplotlib.pyplot as plt

df['年齢'].hist(bins=5)  # 年齢のヒストグラム
plt.show()
```
- `hist()` → **ヒストグラムを作成**
- `plt.show()` → **グラフを表示**

 **結果：年齢の分布が視覚化できる** 

---

## **6. Pandas を使うメリット**
 **データの操作が簡単（Excel や SQL のような操作ができる）**  
 **NumPy を内部で使っているので高速**  
 **Jupyter Notebook などで使うと出力が見やすい**  
 **データの読み書き（CSV, Excel, SQL など）が簡単**  

---

## **7. Pandas のインストール**
Pandas を使うには、事前にインストールが必要です。

```sh
pip install pandas
```
Jupyter Notebook などで使う場合は、以下のコマンドでインストールできます。
```sh
pip install pandas matplotlib seaborn
```

---

## **8. まとめ**
| 操作 | コマンド |
|------|---------|
| Pandas のインポート | `import pandas as pd` |
| CSV 読み込み | `pd.read_csv("data.csv")` |
| CSV 書き出し | `df.to_csv("output.csv")` |
| データ確認 | `df.head()`, `df.info()`, `df.describe()` |
| データのフィルタリング | `df[df['年齢'] >= 25]` |
| データのグループ化 | `df.groupby('職業')['年齢'].mean()` |
| 欠損値の処理 | `df.dropna()`, `df.fillna(値)` |
| 可視化 | `df['年齢'].hist()` |

