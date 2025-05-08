`Number.EPSILON` は、JavaScript の **浮動小数点計算における「最小誤差」**（≒比較用の最小差）を表す **定数**です。

---

## 値

```javascript
console.log(Number.EPSILON); // 2.220446049250313e-16
```

これは JavaScript が内部で使用する IEEE 754 の \*\*倍精度浮動小数点数（double precision）\*\*において、
**1 とそれより大きい最小の数との差**を意味します。

---

## 使いどころ

### なぜ必要なのか？

JavaScript の浮動小数点計算は**正確でない**ことがあります：

```javascript
console.log(0.1 + 0.2);  // → 0.30000000000000004
```

これにより、次のような比較は **false** になります：

```javascript
console.log(0.1 + 0.2 === 0.3);  // false!
```

### どう使うのか？

`Number.EPSILON` を使って、「誤差の許容範囲内か」を判定します：

```javascript
function nearlyEqual(a, b) {
    return Math.abs(a - b) < Number.EPSILON;
}

console.log(nearlyEqual(0.1 + 0.2, 0.3));  // true!
```

---

## EPSILON の意味

* 「Epsilon（エプシロン）」は数学で「限りなく小さい正の数」を表す記号です。
* `Number.EPSILON` も、「**誤差を比較するための最小単位**」と考えるとよいです。

---

## EPSILON を使うことでできること

* 浮動小数点同士の安全な比較
* 四捨五入時の誤差補正（例：`Math.round((num + Number.EPSILON) * 100) / 100`）
* 科学技術計算や金額計算での「誤差吸収」

---

## 注意点

* `Number.EPSILON` は非常に小さいため、比較対象によっては **もっと大きな許容誤差**が必要になる場合があります：

```javascript
function nearlyEqual(a, b, epsilon = Number.EPSILON * Math.max(1, Math.abs(a), Math.abs(b))) {
    return Math.abs(a - b) < epsilon;
}
```

---

## まとめ

| 特徴  | 内容                                 |
| --- | ---------------------------------- |
| 値   | 約 `2.22e-16`                       |
| 意味  | 1 とそれより大きい最小の数の差（≒誤差の最小単位）         |
| 用途  | 浮動小数点比較の精度補正、誤差吸収                  |
| 使用例 | `Math.abs(a - b) < Number.EPSILON` |

---
