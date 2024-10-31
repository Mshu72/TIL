HTMLのテーブルにソート機能を追加するには、JavaScriptを使って特定の列を昇順や降順に並べ替える機能を実装します。以下にシンプルな例を示します。

### 手順

1. **HTMLテーブル**を作成し、ソートしたい列のヘッダーにクリックイベントを追加します。
2. **JavaScript**で、クリックされた列に基づいてソートを実行します。

### サンプルコード

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>テーブルのソート機能</title>
<style>
    table {
        width: 100%;
        border-collapse: collapse;
    }
    th, td {
        padding: 8px;
        border: 1px solid #ddd;
        text-align: left;
        cursor: pointer;
    }
</style>
</head>
<body>

<h2>テーブルのソート機能</h2>
<table id="myTable">
    <thead>
        <tr>
            <th onclick="sortTable(0)">名前</th>
            <th onclick="sortTable(1)">年齢</th>
            <th onclick="sortTable(2)">職業</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>田中太郎</td>
            <td>28</td>
            <td>エンジニア</td>
        </tr>
        <tr>
            <td>佐藤花子</td>
            <td>34</td>
            <td>デザイナー</td>
        </tr>
        <tr>
            <td>鈴木次郎</td>
            <td>41</td>
            <td>マネージャー</td>
        </tr>
        <tr>
            <td>山本真一</td>
            <td>22</td>
            <td>エンジニア</td>
        </tr>
    </tbody>
</table>

<script>
let sortDirection = true; // true = 昇順, false = 降順

function sortTable(columnIndex) {
    const table = document.getElementById("myTable");
    const tbody = table.tBodies[0];
    const rows = Array.from(tbody.rows);

    rows.sort((rowA, rowB) => {
        const cellA = rowA.cells[columnIndex].innerText;
        const cellB = rowB.cells[columnIndex].innerText;

        // 年齢列は数値で比較、それ以外は文字列で比較
        if (columnIndex === 1) {
            return sortDirection ? cellA - cellB : cellB - cellA;
        } else {
            return sortDirection ? cellA.localeCompare(cellB) : cellB.localeCompare(cellA);
        }
    });

    // ソート結果を反映
    rows.forEach(row => tbody.appendChild(row));

    // ソート方向を切り替える
    sortDirection = !sortDirection;
}
</script>

</body>
</html>
```

### 説明

1. **HTMLテーブル**：各`th`要素に`onclick="sortTable(列インデックス)"`を設定しています。これにより、ユーザーが列ヘッダーをクリックするとその列に基づいてソートが行われます。

2. **JavaScript関数 `sortTable`**：
   - `columnIndex`はクリックされた列のインデックスです。
   - `sortDirection`はソートの方向（昇順または降順）を管理するためのフラグです。
   - `rows.sort()`メソッドを使って、選択された列の値を基準にソートします。年齢列（数値）の場合は数値で比較し、それ以外は文字列で比較します。
   - 最後にソート方向を切り替えることで、次回クリック時には逆のソート順に切り替わります。

### 応用

このサンプルをカスタマイズして、複数列を一度にソートしたり、ソートアイコン（昇順や降順の矢印）を追加して視覚的に表示することも可能です。
