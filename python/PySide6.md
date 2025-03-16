### PySide6 とは？
PySide6 は、**Qt for Python** の公式バインディングであり、Python から Qt6 の機能を利用できる GUI (グラフィカルユーザーインターフェース) フレームワークです。**Qt Company** によって提供されており、PyQt6 と並んで Python で Qt を使う主要なライブラリの一つです。

---

##  **特徴**
### 1. **Qt6 ベース**
PySide6 は Qt6 の機能を Python で扱えるようにしたライブラリで、クロスプラットフォーム対応 (Windows, macOS, Linux) しています。

### 2. **公式サポート**
Qt Company 公式の Python バインディングであり、ライセンスは **LGPL** や **商用ライセンス** があります。

### 3. **QtDesigner との連携**
QtDesigner で作成した `.ui` ファイルを Python で利用でき、視覚的に UI を設計しやすいです。

### 4. **QML 対応**
QML (Qt Modeling Language) を使って、モダンな UI を作成できます。

### 5. **PyQt との違い**
| 比較項目 | PySide6 | PyQt6 |
|----------|--------|-------|
| 提供元 | Qt Company | Riverbank Computing |
| ライセンス | LGPL / 商用 | GPL / 商用 |
| API | Qt6 準拠 | Qt6 準拠 |
| シグナル・スロットの定義方法 | デコレーター使用なし | `pyqtSignal` を使用 |
| ドキュメント | Qt公式に統合 | 独自のドキュメント |

PySide6 は Qt6 の公式サポートを受けているため、Qt の新機能への対応が速い傾向があります。

---

##  **インストール**
```sh
pip install PySide6
```

**バージョン確認**
```sh
python -c "import PySide6; print(PySide6.__version__)"
```

---

##  **基本的なウィンドウアプリの作成**
### ① **シンプルなウィンドウ**
```python
import sys
from PySide6.QtWidgets import QApplication, QWidget

app = QApplication(sys.argv)

# ウィンドウの作成
window = QWidget()
window.setWindowTitle("PySide6 簡単なウィンドウ")
window.resize(400, 300)
window.show()

sys.exit(app.exec())
```
このコードを実行すると、400x300 のウィンドウが表示されます。

---

##  **主要コンポーネント**
### 1. **QMainWindow (メインウィンドウ)**
```python
from PySide6.QtWidgets import QApplication, QMainWindow

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("メインウィンドウ")

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

### 2. **QPushButton (ボタン)**
```python
from PySide6.QtWidgets import QApplication, QPushButton, QWidget, QVBoxLayout

class MainWindow(QWidget):
    def __init__(self):
        super().__init__()

        layout = QVBoxLayout()
        self.button = QPushButton("クリックしてね！")
        self.button.clicked.connect(self.button_clicked)
        layout.addWidget(self.button)

        self.setLayout(layout)

    def button_clicked(self):
        print("ボタンがクリックされました！")

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

---

##  **シグナル・スロット**
PySide6 では、シグナル・スロット機能を使ってイベントを処理できます。

### **例: ボタンのクリックイベント**
```python
from PySide6.QtWidgets import QApplication, QPushButton, QWidget

class MyWindow(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("シグナル・スロットの例")

        self.button = QPushButton("押してみて！", self)
        self.button.clicked.connect(self.on_button_clicked)

    def on_button_clicked(self):
        print("ボタンが押されました！")

app = QApplication([])
window = MyWindow()
window.show()
app.exec()
```
`clicked.connect(self.on_button_clicked)` で、ボタンのクリック時に `on_button_clicked` 関数が呼ばれます。

---

##  **QML を利用した UI**
PySide6 では **QML** (Qt Modeling Language) を使ってモダンな UI を作成できます。

### **QML ファイル (main.qml)**
```qml
import QtQuick 6.2
import QtQuick.Controls 6.2

ApplicationWindow {
    visible: true
    width: 400
    height: 300
    title: "QML と PySide6"

    Button {
        text: "クリック"
        anchors.centerIn: parent
        onClicked: console.log("ボタンがクリックされました！")
    }
}
```

### **Python で QML を読み込む**
```python
from PySide6.QtWidgets import QApplication
from PySide6.QtQuick import QQuickView
from PySide6.QtCore import QUrl

app = QApplication([])
view = QQuickView()
view.setSource(QUrl("main.qml"))
view.show()
app.exec()
```
QML で UI を設計し、Python で動作を制御することができます。

---

##  **まとめ**
 **PySide6 は Qt6 ベースの公式 GUI フレームワーク**  
 **クロスプラットフォーム対応 (Windows, macOS, Linux)**  
 **QtDesigner や QML で UI 作成が可能**  
 **PyQt6 と似ているが、公式サポートあり**  
 **シグナル・スロットを使ったイベント処理が簡単**  
