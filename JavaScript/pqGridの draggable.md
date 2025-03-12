`pqGrid` の `draggable` 機能について詳しく解説します。  

## **pqGrid の draggable とは？**
`pqGrid` には、行（row）やセル（cell）をドラッグできる **「draggable（ドラッグ可能）」** な機能が用意されています。  
この機能を使うと、  
**行をドラッグして別の `pqGrid` にドロップ** したり、  
**セルをドラッグして順番を変更** したりできます。  

主に `rowDrag` や `rowDrop` などのオプションを設定して利用します。  

---

## **基本的な設定方法**
`draggable` の機能は **行単位** で使うことが多いので、まずは行をドラッグする方法を紹介します。  

### **1. `rowDrag` を使った行のドラッグ**
`rowDrag: { on: true }` を設定すると、行をドラッグできるようになります。  
```javascript
$("#grid").pqGrid({
  dataModel: {
    data: [
      { id: 1, name: "田中" },
      { id: 2, name: "佐藤" }
    ]
  },
  colModel: [
    { title: "ID", dataIndx: "id", width: 100 },
    { title: "名前", dataIndx: "name", width: 200 }
  ],
  rowDrag: {
    on: true, // 行のドラッグを有効化
  }
});
```
**この設定だけで、行をドラッグできるようになります！**  
**しかし、ドロップ先がないと移動できない** ので、次に `rowDrop` を設定します。

---

### **2. `rowDrop` を使った行のドロップ**
`rowDrop: { on: true }` を設定すると、行をドロップできます。  
例えば、**2つの `pqGrid` の間で行を移動する場合**、次のように設定します。

#### **子画面（ドラッグ元）**
```javascript
$("#childGrid").pqGrid({
  dataModel: { data: childData },
  colModel: [
    { title: "ID", dataIndx: "id" },
    { title: "名前", dataIndx: "name" }
  ],
  rowDrag: {
    on: true // 行をドラッグ可能に
  }
});
```

#### **親画面（ドロップ先）**
```javascript
$("#parentGrid").pqGrid({
  dataModel: { data: parentData },
  colModel: [
    { title: "ID", dataIndx: "id" },
    { title: "名前", dataIndx: "name" }
  ],
  rowDrop: {
    on: true, // 行のドロップを有効化
    drop: function (event, ui) {
      let rowData = ui.rowData; // ドラッグされたデータ

      // 親gridにデータを追加
      let grid = $("#parentGrid").pqGrid("getInstance").grid;
      grid.addRow({ rowData: rowData });

      // 子gridから削除
      let childGrid = $("#childGrid").pqGrid("getInstance").grid;
      childGrid.deleteRow({ rowIndx: ui.rowIndx });
    }
  }
});
```

 **この設定をすれば、ドラッグ＆ドロップで行を移動できます！** 

---

## **draggable を使うときのポイント**
- `rowDrag: { on: true }` だけでは **移動先がないと動かせない**  
- `rowDrop: { on: true }` を設定して、ドロップ先を用意する  
- `drop` イベントで **データの削除や追加** を適切に処理する  

---

## **発展的な使い方**
### **1. ドラッグ時のカスタマイズ**
ドラッグ中の見た目を変えたり、特定の条件でドラッグを制限できます。  
例えば、`beforeStart` を使って特定の行だけドラッグ可能にできます。

```javascript
rowDrag: {
  on: true,
  beforeStart: function(event, ui) {
    // IDが1の行はドラッグ不可
    if (ui.rowData.id === 1) {
      return false;
    }
  }
}
```

---

### **2. 他の要素にドロップ**
`pqGrid` 以外の場所（例えば `<div>` や `<ul>`）にドロップすることも可能です。  
その場合は、`connectWith` を使って他の要素と連携できます。

```javascript
rowDrag: {
  on: true,
  connectWith: "#myList" // 他のHTML要素（例: <ul>）と接続
}
```

---

## **まとめ**
 `pqGrid` の `draggable` は `rowDrag` を使うと簡単に実装できる！  
 `rowDrop` を組み合わせると **2つの `pqGrid` 間で行の移動が可能**  
 `beforeStart` を使うと **特定の条件でドラッグを制御** できる  
 `connectWith` を使うと **他の要素にもドロップ可能**  

