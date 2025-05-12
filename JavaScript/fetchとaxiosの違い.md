`fetch` と `axios` はどちらも **HTTPリクエストを送るためのJavaScriptライブラリ/機能**ですが、以下のような違いがあります。

---

## 基本の違い

| 比較項目      | `fetch`                  | `axios`                |
| --------- | ------------------------ | ---------------------- |
| 提供元       | ブラウザ組み込み（標準API）          | サードパーティ製ライブラリ          |
| デフォルト対応   | JSONなどの変換は手動で必要          | 自動でJSON変換される           |
| リクエスト取消   | `AbortController`で可能（面倒） | `axios.CancelToken`で簡単 |
| エラーハンドリング | 200番台以外はエラーとならない         | HTTPステータスで自動的にエラー扱い    |
| 対応ブラウザ    | モダンブラウザのみ                | IEなども対応（polyfillあり）    |

---

## 使用例の違い

### `fetch` の例

```javascript
fetch("https://api.example.com/data")
  .then(response => {
    if (!response.ok) {
      throw new Error("HTTPエラー: " + response.status);
    }
    return response.json(); // 手動でJSONに変換
  })
  .then(data => console.log(data))
  .catch(error => console.error("Fetchエラー:", error));
```

### `axios` の例

```javascript
import axios from "axios";

axios.get("https://api.example.com/data")
  .then(response => {
    console.log(response.data); // 自動でJSON変換
  })
  .catch(error => {
    console.error("Axiosエラー:", error);
  });
```

---

## axios のメリット

* デフォルトで `JSON` 変換してくれる
* ステータスコード（404など）を自動で例外にする
* タイムアウト、リクエストキャンセル、インターセプタ（共通ヘッダやエラーハンドリング）などが簡単に使える
* リクエストとレスポンスのデータ形式をカスタマイズしやすい

---

## fetch のメリット

* ブラウザ標準API（追加ライブラリ不要）
* 小規模・簡単なアプリに向いている
* 近年は機能が充実しており、`AbortController` や `stream` など最新APIにも対応

---

## まとめ：どちらを使うべき？

| 用途                   | おすすめ    |
| -------------------- | ------- |
| 小規模アプリ／外部ライブラリ不要     | `fetch` |
| 中〜大規模アプリ／エラーハンドリング重視 | `axios` |
| 高度な通信制御が必要           | `axios` |

---
