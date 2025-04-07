`pqGrid`では見た目や動作を細かく制御するために `cellClass` や `pq_attr` を使うことがあります。それぞれの意味と使い方を解説します。

---

##  `cellClass` とは？

`cellClass` は、セルに適用する CSS クラス名を指定するためのプロパティです。セルごとに異なる見た目を適用したいときに使います。

### 記述例

```javascript
colModel: [
  {
    title: "ステータス",
    dataIndx: "status",
    width: 100,
    cellClass: function(ui){
      if(ui.rowData.status === "完了") {
        return "status-complete";
      } else {
        return "status-pending";
      }
    }
  }
]
```

### 補足
- 関数を指定すると、行データ（`ui.rowData`）に基づいてクラス名を動的に変更できます。
- クラスは CSS に定義しておきます。

```css
.status-complete {
  background-color: #d4edda;
}
.status-pending {
  background-color: #f8d7da;
}
```

---

##  `pq_attr` とは？

`pq_attr` は、HTML の属性（`data-*` や `title`、`style` など）をセルに付加するためのプロパティです。主にツールチップやカスタム属性など、見た目以外の制御にも使えます。

### 記述例

```javascript
colModel: [
  {
    title: "メモ",
    dataIndx: "note",
    width: 200,
    pq_attr: function(ui){
      return {
        "title": ui.cellData, // ツールチップに表示
        "style": "color: red;" // テキスト色変更
      };
    }
  }
]
```

### 補足
- 戻り値としてオブジェクトを返し、属性名と値のペアを指定します。
- 動的に属性を変えることができ、視覚的な情報や補助情報の付加に便利です。

---

## 違いと使い分け

| 機能     | `cellClass`                             | `pq_attr`                                 |
|----------|------------------------------------------|--------------------------------------------|
| 用途     | CSS クラス適用（スタイルの切り替え）     | HTML属性の設定（title, data-*, styleなど） |
| 書式     | クラス名（または関数で返す）              | 属性オブジェクト（または関数で返す）       |
| 主な目的 | 見た目の制御（色、背景など）              | 補助情報（ツールチップ、データ属性）       |

---

## よくある活用例

- **条件付きセル色分け** → `cellClass`
- **セルにツールチップを表示** → `pq_attr` で `title` 指定
- **アクセシビリティ対応や独自データ付与** → `pq_attr` で `data-*` 追加

