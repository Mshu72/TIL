HTMLの`target="_blank"`は、リンクを「**新しいタブまたは新しいウィンドウ**」で開くように指定する属性です。   
ただし、実際に**新しいタブになるか新しいウィンドウになるか**は、ユーザーのブラウザやその設定（あるいは拡張機能）に依存します。

### つまり：
- `target="_blank"` → 新しいタブ or 新しいウィンドウ（ブラウザが決定）
- **「確実に新しいウィンドウ」で開かせる方法は、HTMLだけでは制御が難しい**です。

---

### JavaScriptを使えば、別ウィンドウを指定して開くことが可能です：

```html
<a href="https://example.com" onclick="window.open(this.href, 'newwindow', 'width=800,height=600'); return false;">別ウィンドウで開く</a>
```

この例では：
- `window.open()` を使って、幅800px×高さ600pxのウィンドウを新しく開きます。
- `return false;` で、リンクの通常の動作をキャンセルします。

---

### 注意点：
- 最近のブラウザでは、**ポップアップブロック**があるため、ユーザーの操作（クリックなど）以外での新しいウィンドウ表示はブロックされることがあります。
- UX的にも、勝手にウィンドウを開くと不快に感じるユーザーもいるので、適切に使うことが大切です。

