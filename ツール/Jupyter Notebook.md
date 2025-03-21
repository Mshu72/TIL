## **Jupyter Notebookとは？**
**Jupyter Notebook** は、データ分析、機械学習、プログラミング学習などに広く使われる **インタラクティブな開発環境** です。Pythonをはじめとする複数の言語をサポートし、コード、テキスト、画像、グラフなどを1つのドキュメントにまとめて実行・共有できます。

---

## **1. Jupyter Notebook の特徴**
 **インタラクティブなコード実行**  
→ セル単位でコードを実行できるため、デバッグや実験がしやすい。

 **Markdown対応**  
→ ノートブック内で説明文や数式（LaTeX形式）を記述可能。

 **可視化が簡単**  
→ `matplotlib`, `seaborn`, `plotly` などのライブラリを使ってグラフを表示できる。

 **ブラウザベース**  
→ Webブラウザで動作するため、GUIのインストール不要。

 **複数のプログラミング言語に対応**  
→ Python以外にも、R, Julia, Scala などのカーネル（バックエンド）を追加可能。

 **共有が簡単**  
→ `.ipynb` 形式のファイルを共有すれば、他の人も同じノートブックを実行できる。

---

## **2. Jupyter Notebook のインストール**
Jupyter Notebook は **`pip` や `conda` で簡単にインストール** できます。

### **(1) `pip` でインストール**
```bash
pip install notebook
```

### **(2) `conda` でインストール**
Anaconda 環境を使っている場合:
```bash
conda install -c conda-forge notebook
```

### **(3) Jupyter Notebook の起動**
```bash
jupyter notebook
```
→ ブラウザが自動的に開き、Jupyterのホーム画面が表示されます。

---

## **3. Jupyter Notebook の基本的な使い方**
### **(1) ノートブックの作成**
1. Jupyter Notebook を起動 (`jupyter notebook`)
2. ブラウザで開いたら、`New` ボタンをクリック
3. `Python 3` を選択して新しいノートブックを作成

---

### **(2) セルの種類**
Jupyter Notebook は **セル（cell）** という単位でコードやテキストを記述します。

| セルの種類 | 説明 |
|-----------|------------|
| **Code** | Pythonコードを記述し、実行可能 |
| **Markdown** | 説明文や数式（LaTeX）を記述可能 |
| **Raw** | フォーマットされないプレーンテキスト |

---

### **(3) セルの実行**
コードを実行するには `Shift + Enter` を押すと、セルの内容が実行され、出力が表示されます。

---

### **(4) Markdown の活用**
Jupyter Notebook では **Markdown** を使って説明文を記述できます。

#### **見出し**
```markdown
# 見出し1
## 見出し2
### 見出し3
```

#### **リスト**
```markdown
- リスト1
- リスト2
  - サブリスト
```

#### **数式（LaTeX）**
```markdown
$$E = mc^2$$
```
表示結果:  
\[ E = mc^2 \]

---

## **4. 主要なショートカットキー**
| ショートカット | 説明 |
|--------------|----------|
| `Shift + Enter` | セルを実行し、次のセルへ移動 |
| `Ctrl + Enter` | セルを実行（セルの位置は変わらない） |
| `Esc` + `A` | 上にセルを追加 |
| `Esc` + `B` | 下にセルを追加 |
| `Esc` + `M` | セルを Markdown に変更 |
| `Esc` + `Y` | セルを Code に変更 |
| `Esc` + `D D` | セルを削除 |

---

## **5. Python のデータ可視化**
Jupyter Notebook では、**データの可視化が簡単** にできます。

### **(1) `matplotlib` を使ったグラフの描画**
```python
import matplotlib.pyplot as plt

# データ
x = [1, 2, 3, 4, 5]
y = [10, 20, 25, 30, 50]

# グラフを描画
plt.plot(x, y)
plt.xlabel('X軸')
plt.ylabel('Y軸')
plt.title('サンプルグラフ')
plt.show()
```

---

### **(2) `pandas` を使ったデータ分析**
```python
import pandas as pd

# サンプルデータ
data = {'Name': ['Alice', 'Bob', 'Charlie'], 'Age': [25, 30, 35]}
df = pd.DataFrame(data)

# データフレームを表示
df
```
 **Jupyter Notebook では `print(df)` を使わなくても `df` と入力するだけで表として表示される！**

---

## **6. Jupyter Notebook の拡張機能**
Jupyter Notebook には、さまざまな拡張機能（`nbextensions`）を追加できます。

### **(1) `nbextensions` のインストール**
```bash
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
```

### **(2) `nbextensions` の有効化**
Jupyter Notebook を開いて、**「Nbextensions」タブ** で拡張機能を有効化。

**便利な拡張機能**
- **Table of Contents**（目次を自動生成）
- **Execute Time**（セルの実行時間を表示）
- **Variable Inspector**（変数の中身を可視化）

---

## **7. Jupyter Notebook を `.py` や `.html` に変換**
Jupyter Notebook で作成した `.ipynb` ファイルを **PythonスクリプトやHTMLに変換** することもできます。

### **(1) Pythonスクリプトに変換**
```bash
jupyter nbconvert --to script notebook.ipynb
```
→ `notebook.py` に変換される。

### **(2) HTMLに変換**
```bash
jupyter nbconvert --to html notebook.ipynb
```
→ `notebook.html` が生成される。

---

## **8. Jupyter Notebook と Jupyter Lab の違い**
| | **Jupyter Notebook** | **Jupyter Lab** |
|--------------|----------------|----------------|
| **UI** | シンプル | タブ型で拡張性が高い |
| **複数ファイル** | 1つのノートブックのみ | 複数ノートブックを同時に開ける |
| **機能** | 最低限の機能 | エディタ、ターミナル、拡張機能が充実 |

 **最近では Jupyter Lab が推奨されている！**  
→ `pip install jupyterlab` でインストールし、`jupyter lab` で起動。

---

## **9. まとめ**
- **Jupyter Notebook はインタラクティブな開発環境**
- **Pythonコードの実行やMarkdownの記述が可能**
- **データ分析・可視化が簡単**
- **拡張機能を使うとさらに便利**
- **最近は Jupyter Lab の利用も増えている**
