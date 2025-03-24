`pqGrid`（ParamQuery Grid）は、JavaScriptベースの高機能データグリッドで、スプレッドシートのような操作が可能なライブラリです。  
その中の `selectionModel` は、グリッド上で **どのように行やセルを選択できるかを制御する設定** です。

---

## 基本構文

```javascript
selectionModel: {
    type: 'row',       // 'row', 'cell', 'block', 'column'
    mode: 'single'     // 'single', 'multiple'
}
```

---

## パラメータの詳細

### `type`
選択の「単位」を指定します。

| 値 | 意味 |
|----|------|
| `'row'` | 行単位で選択 |
| `'cell'` | セル単位で選択 |
| `'block'` | セルの矩形範囲を選択（Excelのようなブロック選択） |
| `'column'` | 列単位で選択 |

---

### `mode`
選択の「数」を制御します。

| 値 | 意味 |
|----|------|
| `'single'` | 1つだけ選択可能（行・セル・列） |
| `'multiple'` | 複数選択可能（CtrlやShiftキー併用） |

---

## 使用例

### 行選択（単一）

```javascript
selectionModel: {
    type: 'row',
    mode: 'single'
}
```

→ ユーザーは1行だけ選択できます。

---

### 行選択（複数）

```javascript
selectionModel: {
    type: 'row',
    mode: 'multiple'
}
```

→ Ctrl や Shift を使って複数行選択が可能。

---

### セル選択（ブロック）

```javascript
selectionModel: {
    type: 'block',
    mode: 'multiple'
}
```

→ マウスでドラッグして複数セル（ブロック）選択可能。Excelっぽい操作ができます。

---

## 補足：選択状態の取得・操作

```javascript
var selected = $grid.pqGrid('selection', { type: 'row', method: 'getSelection' });
```

`getSelection` で現在選択中の行やセルの情報を取得できます。

---

## よくある用途

- 選択した行を使って編集画面を開く
- 複数行選択 → 一括削除や一括操作
- セル選択 → コピペ機能や値チェック
