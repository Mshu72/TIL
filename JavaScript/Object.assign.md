`Object.assign` は、JavaScriptでオブジェクトを操作するときによく使う **プロパティのコピー・マージ**のための便利なメソッドです。

---

## 基本構文

```javascript
Object.assign(target, ...sources)
```

### ✔ 説明：
- `target`：プロパティを **受け取る**（上書きされる）オブジェクト
- `sources`：プロパティを **提供する** オブジェクト（複数渡せる）

---

## どう動くの？

```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

Object.assign(target, source);
// → target は { a: 1, b: 4, c: 5 }
```

### ポイント：
- `source` のプロパティが `target` に上書きされる（b が 2 → 4 に）
- `c` は `target` に存在しなかったので追加される
- `target` 自体が変わる（破壊的操作）

---

## よくある用途

### 1. オブジェクトのマージ
```javascript
const merged = Object.assign({}, obj1, obj2); // obj1 と obj2 をマージ
```

### 2. デフォルト値の設定
```javascript
const defaultOptions = { darkMode: false, language: "ja" };
const userOptions = { darkMode: true };
const options = Object.assign({}, defaultOptions, userOptions);
// → { darkMode: true, language: "ja" }
```

### 3. オブジェクトのコピー
```javascript
const original = { x: 1 };
const copy = Object.assign({}, original);
```

---

##  注意点

### 1. ネストしたオブジェクトは**浅いコピー**
```javascript
const obj1 = { nested: { value: 1 } };
const copy = Object.assign({}, obj1);
copy.nested.value = 99;
console.log(obj1.nested.value); // → 99（同じ参照を持っている）
```
➡ 深いコピーが必要なら `structuredClone()` やライブラリ（lodashなど）を使う。

### 2. 配列もオブジェクト扱い
```javascript
Object.assign([1, 2], [3, 4]);
// → [3, 4] に上書きされる（indexベース）
```

---

##  実例
```javascript
Object.assign(row, specificUpdateData[dropFlg]);
```

- グリッドの1行（`row`）に対して、更新すべき項目だけを上書きしています。
- `row` はそのまま書き換わる（再描画対象になる）

