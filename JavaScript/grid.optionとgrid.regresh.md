
```javascript
grid.option('dataModel', dataModel);
grid.refresh();
```

これは、**JavaScriptのUIグリッドライブラリ（たとえば [ParamQuery Grid](https://paramquery.com/)、あるいはそれに似たライブラリ）**でよく使われる構文です。   
以下、それぞれの行を詳しく解説します。

---

###  `grid.option('dataModel', dataModel);`

####  意味：
- グリッドに表示される **データの本体（dataModel）を再設定する処理**です。
- `dataModel` には `data` という配列が含まれていて、それがグリッドの行を構成します。

####  例：
```javascript
{
  data: [
    { eqpId: "A001", eqpNo: 1, floor: "1F" },
    { eqpId: "A002", eqpNo: 2, floor: "2F" }
  ]
}
```

このようなデータを `dataModel` に渡すと、グリッドは2行分の情報を表示します。

---

###  `grid.refresh();`

####  意味：
- **グリッドのUIを再描画（再読み込み）する命令**です。
- `dataModel` を更新しても、それだけでは画面には反映されないため、この `refresh()` を呼び出して **最新のデータで画面を再表示**します。

---

###  セットで使う理由：

この2つは **セットで使われるのが一般的** です。

```javascript
grid.option('dataModel', dataModel); // データを設定
grid.refresh();                      // 表示を更新
```

この流れにより：

- データを書き換える（＝裏で編集されたデータをセット）
- 新しいデータに基づいてグリッドの表示内容を更新する

---

###  実用的なイメージ：
UI操作で一部のデータを初期状態に戻した場合、
この2行が呼ばれてグリッドが即座に最新状態で反映される、というわけです。

---
