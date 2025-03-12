## ** OpenCV（cv2）ライブラリとは？**
**OpenCV（Open Source Computer Vision Library）** は、画像処理やコンピュータービジョンのための **オープンソースライブラリ** です。  
Pythonでは **`cv2`** というモジュール名で利用できます。  

**特徴**  
- 高速な画像処理と解析  
- **顔認識・物体検出・動画処理** などの機能が充実  
- **機械学習やディープラーニングと統合** 可能  
- **C++、Python、Java など複数の言語に対応**  

---

## ** OpenCV（cv2）の主な機能**
### **1️ 画像の読み込み・表示・保存**
```python
import cv2

# 画像を読み込む
img = cv2.imread("sample.jpg")  # BGR形式で読み込まれる

# 画像を表示
cv2.imshow("Image", img)
cv2.waitKey(0)  # キー入力待ち
cv2.destroyAllWindows()  # ウィンドウを閉じる

# 画像を保存
cv2.imwrite("output.jpg", img)
```
 **ポイント**  
- `cv2.imread()` → 画像をBGR形式で読み込む  
- `cv2.imshow()` → 画像を表示  
- `cv2.imwrite()` → 画像を保存  

---

### **2️ 画像の色変換（BGR ⇄ RGB）**
```python
rgb_img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)  # BGR → RGB 変換
gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)  # グレースケール変換
```
 **ポイント**  
- `cv2.COLOR_BGR2RGB` → OpenCVはBGR形式なので、RGBに変換  
- `cv2.COLOR_BGR2GRAY` → グレースケールに変換  

---

### **3️ 画像のリサイズ**
```python
resized_img = cv2.resize(img, (200, 200))  # 200×200ピクセルにリサイズ
```
 **ポイント**  
- `cv2.resize()` で画像のサイズ変更  

---

### **4️ 画像の回転**
```python
(h, w) = img.shape[:2]
center = (w // 2, h // 2)
matrix = cv2.getRotationMatrix2D(center, 45, 1.0)  # 45度回転
rotated_img = cv2.warpAffine(img, matrix, (w, h))
```
 **ポイント**  
- `cv2.getRotationMatrix2D()` で回転行列を取得  
- `cv2.warpAffine()` で回転を適用  

---

### **5️ 画像のフィルタリング（ぼかし・シャープ化）**
```python
# ぼかし（GaussianBlur）
blurred_img = cv2.GaussianBlur(img, (5, 5), 0)

# シャープ化
kernel = np.array([[0, -1, 0], [-1, 5, -1], [0, -1, 0]])
sharpened_img = cv2.filter2D(img, -1, kernel)
```
 **ポイント**  
- `cv2.GaussianBlur()` → 画像をぼかす  
- `cv2.filter2D()` → カーネルを使ってフィルタ処理（シャープ化など）  

---

### **6️ 物体検出（顔検出）**
```python
face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_frontalface_default.xml")

gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
faces = face_cascade.detectMultiScale(gray_img, scaleFactor=1.1, minNeighbors=5)

for (x, y, w, h) in faces:
    cv2.rectangle(img, (x, y), (x + w, y + h), (0, 255, 0), 2)

cv2.imshow("Detected Faces", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
 **ポイント**  
- `cv2.CascadeClassifier()` を使って **事前学習済みモデル（Haar Cascade）** で顔を検出  
- `cv2.rectangle()` で顔の周囲に四角を描画  

---

### **7️ 動画処理（Webカメラ入力）**
```python
cap = cv2.VideoCapture(0)  # 0はカメラデバイス番号

while True:
    ret, frame = cap.read()
    if not ret:
        break

    cv2.imshow("Webcam", frame)

    if cv2.waitKey(1) & 0xFF == ord("q"):
        break

cap.release()
cv2.destroyAllWindows()
```
 **ポイント**  
- `cv2.VideoCapture(0)` → Webカメラを開く  
- `cap.read()` → フレームを取得  
- `cv2.imshow()` → フレームを表示  
- `cv2.waitKey(1) & 0xFF == ord("q")` → `q` を押したら終了  

---

## ** OpenCV（cv2）のインストール**
PythonでOpenCVを使うには、以下のコマンドでインストールできます。  
```sh
pip install opencv-python
```
または、フル機能（GUI関連も含む）が必要なら：
```sh
pip install opencv-python-headless
```
`opencv-python-headless` は、**GUIの表示なしで処理を行う場合に推奨** されます。  

---

## ** まとめ**
| 機能             | 関数                      | 説明 |
|----------------|----------------------|------|
| 画像の読み込み | `cv2.imread()`        | 画像をBGR形式で読み込む |
| 画像の表示     | `cv2.imshow()`        | 画像をウィンドウに表示 |
| 画像の保存     | `cv2.imwrite()`       | 画像をファイルに保存 |
| 色変換         | `cv2.cvtColor()`      | BGR ⇄ RGB, グレースケール変換 |
| 画像のリサイズ | `cv2.resize()`        | 画像サイズを変更 |
| 画像の回転     | `cv2.getRotationMatrix2D() + cv2.warpAffine()` | 画像を回転 |
| ぼかし処理     | `cv2.GaussianBlur()`  | 画像をぼかす |
| シャープ化     | `cv2.filter2D()`      | 画像をシャープ化 |
| 顔検出         | `cv2.CascadeClassifier()` | 事前学習済みモデルを使って顔検出 |
| 動画処理       | `cv2.VideoCapture()`  | Webカメラや動画を処理 |

