### `window.close()` の解説

`window.close()` は JavaScript で現在開いているウィンドウやタブを閉じるためのメソッドです。  
ただし、**スクリプトで開いたウィンドウのみ閉じることができます**。

---

### 基本構文
```javascript
window.close();
```

---

### 例1: ボタンでウィンドウを閉じる
```html
<button onclick="window.close()">ウィンドウを閉じる</button>
```
- ボタンをクリックすると、ウィンドウが閉じます。  
- ただし、このウィンドウが **JavaScript で開かれたもの**である必要があります。

---

### 例2: 新しいウィンドウを開いて自動で閉じる
```javascript
const newWin = window.open('https://www.example.com', '_blank', 'width=500,height=400');
setTimeout(function() {
    newWin.close();
}, 3000);  // 3秒後にウィンドウを閉じる
```
- 新しいウィンドウを開き、3秒後に自動的に閉じます。

---

### 動作する場合
- `window.open()` で開いたウィンドウやタブ。  
- ポップアップウィンドウ。  

---

### 動作しない場合
- **ユーザーが手動で開いたウィンドウやタブ**は、`window.close()` では閉じられません。  
- **ブラウザの設定**や**ポップアップブロッカー**が有効な場合も閉じられないことがあります。  
- Chromeなど一部のブラウザでは、`window.close()` が**ユーザー操作を伴わない**と機能しません。

---

### 回避方法
#### 1. ポップアップウィンドウをスクリプトで開いて閉じる
```javascript
function openAndClose() {
    const win = window.open('', '', 'width=300,height=200');
    win.document.write('<p>このウィンドウは自動で閉じます。</p>');
    setTimeout(() => win.close(), 2000);
}
```

#### 2. ユーザーに閉じるよう促す
```javascript
function closeWindow() {
    alert("このウィンドウは自動で閉じられません。手動で閉じてください。");
}
```

---

### `window.close()` が効かない場合の原因
1. **スクリプトで開いていないウィンドウ**  
   例: ユーザーが直接開いたタブやウィンドウ。  
   
2. **セキュリティ制限**  
   ユーザーが意図しないウィンドウを勝手に閉じないよう、ブラウザが制限しています。  

3. **ポップアップブロック**  
   特に Chrome では、ポップアップがブロックされやすく、`window.close()` が動作しません。  

---

### 確実に動かす方法
- **`window.open()` で開いたウィンドウのみ閉じることが可能**。  
- **ユーザーのクリックイベント**などをトリガーにして `window.close()` を呼び出せば、ポップアップブロックを回避できます。

例:  
```html
<button id="openBtn">ポップアップを開いて閉じる</button>

<script>
document.getElementById('openBtn').addEventListener('click', function() {
    const win = window.open('https://www.example.com', '_blank', 'width=400,height=300');
    setTimeout(() => win.close(), 2000);
});
</script>
```

---

### まとめ
- **`window.close()` はスクリプトで開いたウィンドウを閉じるためのメソッド。**  
- **ユーザーが開いたウィンドウには基本的に使えない。**  
- **ブラウザのセキュリティ制限が強いため、ポップアップを開いたスクリプト内で閉じる方法が最も確実。**
