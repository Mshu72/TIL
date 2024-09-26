親項目を選択すると下部に子項目が展開され、親項目右端の「＜」マークが90度反時計回りに回転するメニューを作成するためのHTML、CSS、およびJavaScriptのコードを紹介します。

以下のコードを参考にしてください。
```
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ドロップダウンメニュー</title>
    <style>
        .menu {
            list-style: none;
            padding: 0;
            margin: 0;
        }
        .menu-item {
            position: relative;
            padding: 10px;
            border: 1px solid #ccc;
            cursor: pointer;
        }
        .menu-item .arrow {
            float: right;
            transition: transform 0.3s;
        }
        .submenu {
            display: none;
            list-style: none;
            padding: 0;
            margin: 0;
            border-top: 1px solid #ccc;
        }
        .menu-item.active .submenu {
            display: block;
        }
        .menu-item.active .arrow {
            transform: rotate(-90deg);
        }
    </style>
</head>
<body>
    <ul class="menu">
        <li class="menu-item">
            親項目1 <span class="arrow">＜</span>
            <ul class="submenu">
                <li>子項目1-1</li>
                <li>子項目1-2</li>
                <li>子項目1-3</li>
            </ul>
        </li>
        <li class="menu-item">
            親項目2 <span class="arrow">＜</span>
            <ul class="submenu">
                <li>子項目2-1</li>
                <li>子項目2-2</li>
                <li>子項目2-3</li>
            </ul>
        </li>
    </ul>

    <script>
        document.querySelectorAll('.menu-item').forEach(item => {
            item.addEventListener('click', () => {
                item.classList.toggle('active');
            });
        });
    </script>
</body>
</html>
```
# 説明
## HTML:
メニュー項目 (menu-item) とサブメニュー (submenu) をリスト (ul) で構成しています。 親項目の右端に「＜」マークを表示するために、＜ を使用しています。

## CSS:
- menu-item に対して基本的なスタイルを設定し、.arrow に対して回転アニメーションを設定しています。
- submenu はデフォルトで非表示にし、.menu-item.active クラスが追加されたときに表示されるようにしています。
- menu-item.active .arrow によって、親項目がアクティブなときに矢印が90度反時計回りに回転するようにしています。
## JavaScript:
各メニュー項目にクリックイベントを追加し、クリックされた項目に active クラスをトグル（追加/削除）しています。
