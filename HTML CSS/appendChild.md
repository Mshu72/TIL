# `appendChild `メソッド
JavaScript で HTML 要素を新たにページに追加するときに使うメソッドです。  
簡単に言うと、ある要素の中に別の要素を追加するための方法です。

## どういうときに使うのか？
例えば、ウェブページに動的に新しいボタンやテキスト、画像などを追加したいときに使います。

## 基本的な使い方
追加したい要素（例: div タグや p タグ）を作る。  

その要素を、既存のページ内の特定の場所に追加する。
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>appendChildの例</title>
</head>
<body>
    <div id="container">ここに新しい要素が追加されます。</div>

    <script>
        // 1. 新しい要素（pタグ）を作成
        let newElement = document.createElement('p');
        
        // 2. 作った要素にテキストを追加
        newElement.textContent = 'これは新しく追加された段落です！';

        // 3. 既存の要素（#container）を取得
        let container = document.getElementById('container');

        // 4. containerに新しい要素を追加
        container.appendChild(newElement);
    </script>
</body>
</html>
```
## 実行結果
上記のコードを実行すると、`div id="container"` の中に新しい段落（`p`タグ）が追加され、「これは新しく追加された段落です！」と表示されます。

# ポイント
- `createElement()` で新しい HTML 要素を作る。
- `textContent` でその要素にテキストを入れることができる。
- `appendChild()` で、その要素をページ内のどこかに追加する。

これを使うことで、ウェブページを動的に変更することができます。
