## CKEditorとは？

**CKEditor（シーケーエディター）**は、ウェブページ上で使える**WYSIWYG（ウィジウィグ）エディター**の一つです。  
※WYSIWYGとは「What You See Is What You Get」の略で、見たまま編集できるエディターのことです。

ウェブアプリケーションにリッチテキスト編集機能（太字、画像挿入、リンクなど）を簡単に追加できるJavaScript製のライブラリです。

---

## 主な特徴

| 特徴 | 説明 |
|------|------|
|  WYSIWYG編集 | 実際の表示に近い形で文章を編集できる |
|  プラグイン構成 | 機能をプラグインとして追加・削除できる |
|  多言語対応 | 多くの言語に対応、日本語ももちろん対応 |
|  画像アップロード対応 | 画像のドラッグ＆ドロップアップロードが可能 |
|  Markdown対応 | Markdownでの入力や変換も可能（プラグインによる） |
|  セキュリティ | XSS対策やHTMLフィルタリング機能も豊富 |

---

## バージョンの違い

### CKEditor 4
- 古くから使われている安定版
- プラグインが豊富
- クラシックエディターのUI（Wordみたいな見た目）

### CKEditor 5（最新版）
- モダンな設計（TypeScriptベース）
- モジュールベースで軽量・高速
- コラボレーション（リアルタイム編集）にも対応
- クラウド対応（公式の有料クラウドサービスもあり）

---

## 基本的な導入例（CDN使用：CKEditor 5）

```html
<!-- ヘッダーで読み込み -->
<script src="https://cdn.ckeditor.com/ckeditor5/39.0.0/classic/ckeditor.js"></script>

<!-- 編集エリア -->
<textarea id="editor"></textarea>

<script>
  ClassicEditor
    .create(document.querySelector('#editor'))
    .then(editor => {
        console.log('エディターが初期化されました', editor);
    })
    .catch(error => {
        console.error('エディターの初期化に失敗しました', error);
    });
</script>
```

---

## よく使われる機能（プラグイン）

- Bold / Italic / Underline（装飾）
- Table（表の作成）
- Image / Media embed（画像・動画の埋め込み）
- Link / Anchor（リンク）
- Undo / Redo（取り消し・やり直し）
- Autosave（自動保存）
- Word count（文字数カウント）

---

## どんなところで使われてる？

- CMS（WordPress、Drupalなど）
- 社内ツール（社内報、報告書）
- ECサイトの製品説明編集
- フォームアプリ（コメント欄、日報入力など）

---

## 補足

- **ライセンス**：基本はオープンソース（GPL/LGPL/MPL）ですが、商用利用やクラウド版は有償のケースもあります。
- **クラウド対応**：公式でコラボレーション用のクラウドエディター（有料）も提供されています。

