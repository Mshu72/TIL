### **Ajax と Fetch の違いについて解説**

#### **1. Ajax とは？**
Ajax（Asynchronous JavaScript and XML）は、**Webページをリロードせずにサーバーとデータのやり取りを行う技術の総称**です。  
Ajax自体は特定の技術ではなく、JavaScript を使って非同期通信を行う手法のことを指します。

**代表的な実装方法**
- `XMLHttpRequest`（XHR）：古くからあるAjaxの実装方法。
- `fetch` API：よりモダンなAjaxの実装方法。

#### **2. Fetch API とは？**
Fetch API は、**非同期通信をよりシンプルな構文で扱えるように設計されたモダンなAPI** です。  
従来の `XMLHttpRequest` よりも柔軟で使いやすく、Promise ベースで動作します。

---

## **Ajax（XMLHttpRequest） vs. Fetch API の違い**

| **比較項目** | **Ajax（XMLHttpRequest）** | **Fetch API** |
|-------------|---------------------------|---------------|
| **記述の簡潔さ** | コールバックを使うため複雑になりがち | Promise ベースでシンプル |
| **レスポンスの型** | `responseText` や `responseXML` を使う | `response.json()` などで簡単に変換可能 |
| **エラーハンドリング** | `onreadystatechange` で状態管理が必要 | `catch()` を使って簡単に処理可能 |
| **同期/非同期** | 同期・非同期両方可能（ただし同期は非推奨） | 非同期のみ |
| **CORS（クロスオリジンリクエスト）** | デフォルトでは制限が多い | CORS に対応（設定可能） |
| **ステータスエラーの処理** | ステータスコードに応じた処理が必要 | HTTPエラーが自動的に Promise に反映されるわけではない（明示的に `response.ok` をチェックする必要がある） |

---

## **実装の比較**

### **① Ajax（XMLHttpRequest） の例**
```javascript
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1", true);
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(JSON.parse(xhr.responseText)); // レスポンスを出力
    }
};
xhr.send();
```
**デメリット**
- 状態管理（`readyState`）を確認する必要があり、可読性が悪い。
- `onreadystatechange` を使うため、コールバックが増えるとコードが複雑になる。

---

### **② Fetch API の例**
```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json();
  })
  .then(data => console.log(data)) // レスポンスを出力
  .catch(error => console.error("Fetch error:", error));
```
**メリット**
- `then()` チェーンで簡潔に記述可能。
- `async/await` と組み合わせるとさらに可読性が向上。

---

## **まとめ**
- `fetch` API は `XMLHttpRequest` よりもシンプルで、最新の JavaScript の開発スタイルに適している。
- `XMLHttpRequest` は古いコードやレガシーシステムで使われているが、モダンな開発では `fetch` を推奨。
- `fetch` API は Promise ベースのため、エラーハンドリングの方法が異なる (`response.ok` をチェックする必要がある)。

**→ これから新しく開発するなら、基本的に Fetch API を使うのがおすすめ！**
