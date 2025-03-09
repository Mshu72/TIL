### **Streamlitとは？**
Streamlitは、Pythonでシンプルかつ直感的に**データアプリケーション**を作成できるオープンソースのフレームワークです。主に**データサイエンスや機械学習の可視化ツール**として活用されており、わずか数行のコードで**インタラクティブなWebアプリ**を作成できます。

---

## **Streamlitの特徴**
###  **簡単な記述でWebアプリを作成**
通常、FlaskやDjangoを使ってWebアプリを作成すると、多くのコードや設定が必要ですが、Streamlitは**Pythonスクリプトを書くだけで自動的にWebアプリ化**できます。

###  **リアルタイムでUIを更新**
Streamlitは、コードを変更すると**即座にリロードされる**ため、手軽に試行錯誤できます。

###  **データ可視化が強力**
Matplotlib、Plotly、Seaborn、Altair などの可視化ライブラリと組み合わせて、**対話的なグラフを簡単に表示**できます。

###  **ウィジェットでインタラクティブな操作**
ボタンやスライダー、セレクトボックスなどの**GUIウィジェット**をPythonコードで手軽に追加できます。

---

## **Streamlitのインストール**
Streamlitはpipで簡単にインストールできます。

```bash
pip install streamlit
```

---

## **基本的な使い方**
### **1. "Hello, World!" アプリ**
Streamlitを使って簡単なアプリを作成するには、以下のようなPythonスクリプトを作成します。

```python
import streamlit as st

st.title("Hello, Streamlit! ")
st.write("これはシンプルなStreamlitアプリです。")
```

### **2. 実行**
作成したPythonスクリプト（例: `app.py`）を以下のコマンドで実行します。

```bash
streamlit run app.py
```
→ **ブラウザが自動的に開き、アプリが表示されます。**

---

## **主なStreamlitの機能**
### **1. テキストの表示**
```python
st.title("タイトル")
st.header("ヘッダー")
st.subheader("サブヘッダー")
st.text("通常のテキスト")
st.markdown("**マークダウン形式のテキスト**")
```

### **2. インタラクティブなウィジェット**
```python
name = st.text_input("名前を入力してください")
age = st.slider("年齢", 0, 100, 25)
agree = st.checkbox("同意します")
button = st.button("クリック")

if button:
    st.write(f"こんにちは、{name}さん！ あなたは {age} 歳ですね。")
```

### **3. データの可視化**
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# ダミーデータ作成
df = pd.DataFrame(
    np.random.randn(20, 3),
    columns=["A", "B", "C"]
)

# 折れ線グラフ
st.line_chart(df)

# Matplotlibを使用したグラフ
fig, ax = plt.subplots()
ax.hist(df["A"], bins=10)
st.pyplot(fig)
```

### **4. ファイルアップロード**
```python
uploaded_file = st.file_uploader("ファイルをアップロードしてください", type=["csv", "xlsx"])

if uploaded_file:
    df = pd.read_csv(uploaded_file)
    st.write(df)
```

---

## **応用例**
### **1. 機械学習モデルのWebアプリ**
- ユーザーがデータをアップロードすると、学習済みモデルで予測し、結果を表示
- `scikit-learn`や`TensorFlow`と組み合わせて利用可能

### **2. 株価データの可視化**
- `yfinance`ライブラリを使ってリアルタイムの株価データを取得し、可視化

```python
import yfinance as yf

ticker = st.text_input("株式ティッカーを入力（例: AAPL）", "AAPL")
stock = yf.Ticker(ticker)
data = stock.history(period="1y")

st.line_chart(data["Close"])
```

---

## **まとめ**
 **StreamlitはPythonで簡単にWebアプリを作れる**  
 **データ可視化や機械学習のデモアプリに最適**  
 **シンプルな記述で、数行のコードでインタラクティブなアプリが作れる**  

