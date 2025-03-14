## **NumPy（ナンパイ）ライブラリとは？**
**NumPy（Numerical Python）** は、**数値計算** を効率的に行うためのPythonライブラリです。  
特に **多次元配列（`ndarray`）の操作** や **線形代数・統計・行列計算** などが得意です。

 **NumPy の特徴**
- **数値データを効率的に処理** できる
- **Python標準のリストよりも高速**
- **行列・ベクトル計算が得意**
- **機械学習・AI・データ分析に必須**
- **pandas・scipy・tensorflow などのライブラリと相性が良い**

---

## **NumPy のインストール**
Python で NumPy を使うには、以下のコマンドでインストールします。
```sh
pip install numpy
```
または、すでに `pandas` や `scipy` などをインストールしている場合、NumPy は自動的にインストールされています。

---

## **NumPy の基本的な使い方**
### **1️ NumPy をインポート**
```python
import numpy as np  # 一般的に "np" という別名で使う
```

---

### **2️ NumPy 配列（ndarray）の作成**
NumPy の基本データ構造は `ndarray（N次元配列）` です。  
Python のリストを `np.array()` で NumPy 配列に変換できます。

```python
import numpy as np

# 1次元配列（ベクトル）
arr1 = np.array([1, 2, 3, 4, 5])
print(arr1)  # [1 2 3 4 5]

# 2次元配列（行列）
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2)
# [[1 2 3]
#  [4 5 6]]

# 3次元配列（テンソル）
arr3 = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
print(arr3)
```
 **ポイント**
- NumPy 配列は Python のリストと似ているが、**計算が高速でメモリ効率が良い**
- `np.array()` を使って **リスト → NumPy 配列** に変換

---

### **3️ 配列の基本操作**
#### **(1) 配列の形状とサイズ**
```python
print(arr2.shape)  # (2, 3) → 2行3列
print(arr2.ndim)   # 2 → 2次元配列
print(arr2.size)   # 6 → 要素の総数
print(arr2.dtype)  # int32（環境による）
```
 **ポイント**
- `.shape` → 配列の形状（行, 列）
- `.ndim` → 配列の次元数
- `.size` → 要素数
- `.dtype` → データ型

---

#### **(2) 配列の要素にアクセス**
```python
print(arr2[0, 1])  # 2 （1行目・2列目の要素）
print(arr2[:, 1])  # [2 5] （すべての行の2列目）
```
 **ポイント**
- `arr[i, j]` → `i` 行 `j` 列の要素を取得
- `:` を使うと **すべての行/列を取得** できる

---

#### **(3) 配列のリサイズ**
```python
arr_reshaped = arr2.reshape(3, 2)
print(arr_reshaped)
# [[1 2]
#  [3 4]
#  [5 6]]
```
 **ポイント**
- `.reshape(行, 列)` で形状を変更

---

### **4️ NumPy の特殊な配列作成**
#### **(1) すべてゼロの配列**
```python
np.zeros((2, 3))  # 2行3列のゼロ行列
```
```
[[0. 0. 0.]
 [0. 0. 0.]]
```

#### **(2) すべて1の配列**
```python
np.ones((3, 3))  # 3×3の1行列
```

#### **(3) ランダムな数値の配列**
```python
np.random.rand(2, 3)  # 0～1の乱数（2×3）
```

#### **(4) 連続した数値の配列**
```python
np.arange(0, 10, 2)  # [0 2 4 6 8]
```
 `np.arange(開始, 終了, ステップ)`

---

### **5 NumPy の計算機能**
NumPy を使うと **ベクトル・行列計算** を簡単に行えます。

#### **(1) 要素ごとの計算**
```python
arr = np.array([1, 2, 3, 4])
print(arr + 10)  # [11 12 13 14]
print(arr * 2)   # [ 2  4  6  8]
print(arr ** 2)  # [ 1  4  9 16]
```
 **ポイント**
- **NumPy は for ループ不要！**
- 配列に対して演算を適用すると **要素ごとに計算** される（ブロードキャスト）

---

#### **(2) 行列計算**
```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(A + B)  # 行列の加算
print(A @ B)  # 行列積（ドット積）
print(np.dot(A, B))  # 同じく行列積
```
 **ポイント**
- `+` → 行列の要素ごとの足し算
- `@` または `np.dot()` → 行列の積（ドット積）

---

#### **(3) 統計計算**
```python
arr = np.array([1, 2, 3, 4, 5])

print(np.mean(arr))  # 平均: 3.0
print(np.median(arr))  # 中央値: 3
print(np.std(arr))  # 標準偏差
print(np.sum(arr))  # 合計: 15
print(np.min(arr))  # 最小値: 1
print(np.max(arr))  # 最大値: 5
```
 **ポイント**
- `np.mean()` → 平均
- `np.median()` → 中央値
- `np.std()` → 標準偏差
- `np.sum()` → 合計
- `np.min()` / `np.max()` → 最小/最大値

---

## **NumPy まとめ**
| 機能 | 関数 | 説明 |
|----|----|----|
| 配列の作成 | `np.array()` | PythonリストをNumPy配列に変換 |
| 配列の形状 | `.shape`, `.ndim`, `.size` | 配列のサイズや次元を取得 |
| 配列の操作 | `reshape()`, `ravel()` | 配列の形状を変更 |
| 特殊な配列 | `np.zeros()`, `np.ones()`, `np.random.rand()` | ゼロ行列、乱数行列の作成 |
| 数学演算 | `np.add()`, `np.multiply()`, `np.dot()` | 行列演算 |
| 統計計算 | `np.mean()`, `np.median()`, `np.std()` | 平均、標準偏差 |

---
