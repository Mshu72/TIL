`pqGrid`の`colModel`は、グリッドに表示する各列の設定を定義するための非常に重要な構成要素です。  
簡単に言えば、**グリッドの「列ごとの設定」を配列で定義するプロパティ**です。

---

##  基本構造

```javascript
colModel: [
  { title: "ID", dataIndx: "id", width: 100 },
  { title: "名前", dataIndx: "name", width: 200 },
  { title: "年齢", dataIndx: "age", width: 80, dataType: "integer" }
]
```

---

## 各プロパティの意味

| プロパティ       | 説明 |
|------------------|------|
| `title`          | 列のヘッダーに表示される名前 |
| `dataIndx`       | データソース（JSONなど）のキーと一致させる必要がある。必須 |
| `width`          | 列の幅（px） |
| `dataType`       | データ型（例：`string`, `integer`, `date`, `float`など） |
| `editable`       | true/falseでセルを編集可能にする |
| `hidden`         | trueで非表示 |
| `align`          | テキストの配置（`left`, `center`, `right`） |
| `cls`            | 列に適用するCSSクラス |
| `render`         | 値をカスタム表示するための関数（例：金額にカンマ付けなど） |
| `editor`         | 入力用エディタの指定（`textbox`, `select`, `checkbox`など） |

---

## 使用例：編集可能なselect列

```javascript
{
  title: "ステータス",
  dataIndx: "status",
  width: 120,
  editor: {
    type: "select",
    options: [
      { "status": "有効", "value": "active" },
      { "status": "無効", "value": "inactive" }
    ]
  },
  render: function(ui){
    return ui.cellData === "active" ? "有効" : "無効";
  }
}
```

---

## よく使うオプションまとめ

- `filter`：列ごとのフィルターを表示（例：`filter: { type: "textbox", condition: 'contain', listeners: ['keyup'] }`）
- `sortType`：ソートの型（例：`"local"`、`"remote"`）
- `summary`：合計・平均などの集計をフッターに表示
- `resizable`：列のリサイズ可否

---

## Tips

- `dataIndx`は**ユニーク**である必要があります。
- `editable`は列ごと、または行ごとに切り替えることも可能です（関数で制御）。
- `colModel`は**列の表示順も制御**します。順番に注意。

