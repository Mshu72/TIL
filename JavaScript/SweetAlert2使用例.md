SweetAlert2の使い方を「よく使われるパターン別」にまとめてご紹介します  

---

# **SweetAlert2 パターン別使い方ガイド**

---

##【1】基本のアラート表示

```javascript
Swal.fire('こんにちは！', 'これはシンプルなアラートです', 'info');
```

- **用途**：メッセージだけを表示したいとき
- **アイコン種類**：`success`, `error`, `warning`, `info`, `question`

---

##【2】確認ダイアログ（Yes/No）

```javascript
Swal.fire({
  title: '削除してもよろしいですか？',
  text: "この操作は元に戻せません！",
  icon: 'warning',
  showCancelButton: true,
  confirmButtonText: 'はい、削除します',
  cancelButtonText: 'キャンセル'
}).then((result) => {
  if (result.isConfirmed) {
    Swal.fire('削除しました！', '', 'success');
  }
});
```

- **用途**：ユーザーに操作確認をしたいとき（削除、送信など）
- **ポイント**：`then()`で条件分岐できる

---

##【3】入力フォーム付きダイアログ

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

- **用途**：名前や情報の入力を受け付ける時
- **inputの種類**：`text`, `email`, `password`, `number`, `textarea`, `select`, など

---

##【4】タイマー付き（自動で閉じる）

```javascript
Swal.fire({
  title: '完了しました！',
  text: '3秒後に閉じます',
  icon: 'success',
  timer: 3000,
  showConfirmButton: false
});
```

- **用途**：通知だけしたいとき（ボタン操作不要）
- **ポイント**：`timer`にミリ秒で時間を指定（例：3000 = 3秒）

---

##【5】カスタムHTMLを表示

```javascript
Swal.fire({
  title: '<strong>お知らせ</strong>',
  html:
    'これは<strong>カスタムHTML</strong>の<br>表示例です😊',
  icon: 'info',
  showCloseButton: true,
  showCancelButton: true,
  focusConfirm: false,
  confirmButtonText: '了解',
  cancelButtonText: 'あとで見る'
});
```

- **用途**：表やリンク、装飾などを含む内容を見せたいとき
- **ポイント**：`html`を使えばHTMLタグがそのまま使える

---

##【6】ローディング・進行中表示

```javascript
Swal.fire({
  title: 'アップロード中...',
  didOpen: () => {
    Swal.showLoading();
  }
});
```

- **用途**：非同期処理中や待機時間に「ぐるぐるマーク」を表示
- **合わせ技**：バックエンド処理と組み合わせて使うと便利

---

##【7】画像付きポップアップ

```javascript
Swal.fire({
  title: 'かわいい猫ちゃん',
  text: 'この画像を見て癒されてください！',
  imageUrl: 'https://placekitten.com/300/200',
  imageWidth: 300,
  imageAlt: '猫の画像'
});
```

- **用途**：画像を表示したい時（紹介・通知・レビューなど）
- **ポイント**：`imageUrl`でURLを指定するだけで簡単に画像表示！

---

##【8】複数ステップのウィザード形式

```javascript
Swal.mixin({
  input: 'text',
  confirmButtonText: '次へ',
  showCancelButton: true,
  progressSteps: ['1', '2', '3']
}).queue([
  {
    title: 'お名前を入力してください'
  },
  {
    title: '年齢を教えてください'
  },
  {
    title: '好きな色は？'
  }
]).then((result) => {
  if (result.value) {
    Swal.fire({
      title: '入力完了！',
      html: `
        名前: ${result.value[0]}<br>
        年齢: ${result.value[1]}<br>
        好きな色: ${result.value[2]}
      `
    });
  }
});
```

- **用途**：フォームを複数段階に分けて聞きたいとき
- **ポイント**：`queue()`で連続ステップを簡単に実装！

---

## 補足：見た目のカスタマイズ

CSSを使って独自のスタイルを当てたり、ボタンの色などもオプションで調整できます！

```javascript
Swal.fire({
  title: 'カスタムボタン',
  icon: 'question',
  confirmButtonColor: '#3085d6',
  cancelButtonColor: '#d33',
  confirmButtonText: 'OK',
  cancelButtonText: 'キャンセル',
  showCancelButton: true
});
```

---

## まとめ

| パターン | 用途 |
|---------|------|
| 基本アラート | 情報通知 |
| 確認ダイアログ | 削除/操作の確認 |
| 入力フォーム | 名前やメールなどの取得 |
| 自動閉じ | 通知メッセージ表示 |
| HTML表示 | 詳細な情報の提示 |
| ローディング | 非同期処理中の表示 |
| 画像付き | ビジュアル通知 |
| ステップ形式 | アンケートや入力フロー |

---

いろんなUIに合わせて柔軟に使えるのがSweetAlert2の魅力です。Webアプリに取り入れると、一気に見栄えが良くなりますよ！
