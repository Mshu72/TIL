**SweetAlert2（スウィートアラート2）**は、JavaScriptで使える**美しくカスタマイズ可能なアラートダイアログライブラリ**です。ブラウザ標準の `alert()` よりもスタイリッシュで、使い勝手が良いのが特徴です。

---

##  SweetAlert2の主な特徴

| 特徴 | 説明 |
|------|------|
|  見た目が美しい | マテリアルデザイン風で、モダンなUIにマッチ |
|  カスタマイズ性抜群 | 色、ボタン、アイコン、HTML挿入など自由自在 |
|  非同期処理対応 | Promise対応で、ユーザーの操作を待つことが可能 |
|  モジュール型 | CDNでもnpmでも利用可能で導入が簡単 |

---

##  基本的な使い方

### 1. CDNで読み込み（HTMLに追加）
```html
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
```

### 2. シンプルなアラートの表示
```javascript
Swal.fire('こんにちは！', 'これはSweetAlert2のメッセージです', 'success');
```

### 3. ユーザーの確認を取るダイアログ
```javascript
Swal.fire({
  title: '本当に削除しますか？',
  text: "この操作は取り消せません！",
  icon: 'warning',
  showCancelButton: true,
  confirmButtonText: 'はい、削除します',
  cancelButtonText: 'キャンセル'
}).then((result) => {
  if (result.isConfirmed) {
    Swal.fire('削除されました！', '', 'success');
  }
});
```

---

##  よく使うオプション

| オプション名 | 内容 |
|-------------|------|
| `title` | タイトル（大きなテキスト） |
| `text` | 内容の説明（小さなテキスト） |
| `icon` | 'success' / 'error' / 'warning' / 'info' / 'question' |
| `showCancelButton` | キャンセルボタンを表示するか |
| `confirmButtonText` | 確認ボタンのラベル |
| `cancelButtonText` | キャンセルボタンのラベル |
| `html` | HTMLで内容を記述（`text`の代わり） |

---

##  応用例：入力フォームつきのポップアップ

```javascript
Swal.fire({
  title: '名前を入力してください',
  input: 'text',
  inputPlaceholder: '山田太郎',
  showCancelButton: true
}).then((result) => {
  if (result.value) {
    Swal.fire(`こんにちは、${result.value}さん！`);
  }
});
```

---

##  インストール（npmで使う場合）

```bash
npm install sweetalert2
```

そしてJavaScriptでインポート：

```javascript
import Swal from 'sweetalert2';
```

---

SweetAlert2は、ユーザー体験を損なわずにアラートや確認ダイアログを表示するのに非常に便利です。特にVue.jsやReactなどのフロントエンドフレームワークと組み合わせて使われることが多いです。

