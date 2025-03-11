`yfinance` は、Yahoo! Finance から株価や市場データを取得するための Python ライブラリです。過去のデータやリアルタイムデータを簡単に取得でき、株式分析やアルゴリズム取引に利用されます。

---

##  **主な機能**
### 1. **株価データの取得**
`yfinance.Ticker` を使用して、特定の銘柄のデータを取得できます。

```python
import yfinance as yf

# 銘柄情報を取得（例：トヨタ 7203.T）
ticker = yf.Ticker("7203.T")

# 最新の株価情報
print(ticker.history(period="1d"))
```

---

### 2. **過去データの取得**
一定期間の過去のデータを取得できます。

```python
# 過去1年分の株価データを取得
df = ticker.history(period="1y")

# データの表示
print(df.head())
```

| Date        | Open  | High  | Low   | Close | Volume |
|------------|-------|-------|-------|-------|--------|
| 2024-03-01 | 2000  | 2050  | 1980  | 2030  | 1000000 |

---

### 3. **リアルタイムデータの取得**
現在の株価や、その他の市場データを取得できます。

```python
print("現在の株価:", ticker.info["currentPrice"])
```

---

### 4. **財務情報の取得**
企業の収益や利益、配当金のデータを取得できます。

```python
# 財務情報
print(ticker.financials)
```

---

### 5. **株主情報の取得**
企業の主要株主情報を取得できます。

```python
print(ticker.major_holders)
```

---

##  **yfinance のインストール**
`yfinance` はデフォルトでインストールされていないため、`pip` でインストールする必要があります。

```sh
pip install yfinance
```

---

##  **注意点**
- Yahoo! Finance の API 仕様変更により、一部のデータが取得できなくなることがあります。
- 無料版の `yfinance` ではリアルタイムデータの更新頻度が限られています。

-
