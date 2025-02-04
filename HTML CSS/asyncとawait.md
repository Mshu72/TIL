

## **1. `async/await` の概要**
`async/await` は、JavaScript の **非同期処理** をより簡潔に書くための構文です。  
従来の **Promise チェーン (`.then()` / `.catch()`) をシンプルに記述できる** ようになります。

---

## **2. `async/await` の基本構文**
### **① `async` 関数**
関数の前に `async` をつけることで、その関数は **常に Promise を返す** 非同期関数になります。

```javascript
async function myFunction() {
  return "Hello, World!";
}

myFunction().then(console.log); // "Hello, World!"
```
`async` をつけると、自動的に Promise が返されるため、`.then()` で処理できます。

---

### **② `await` を使う**
`await` は **Promise が解決されるまで処理を一時停止** し、その結果を変数に代入できます。

```javascript
async function fetchData() {
  let result = await Promise.resolve("Data received!");
  console.log(result);
}

fetchData(); // "Data received!" が表示される
```
📌 `await` のポイント:
- **`await` は `async` 関数の中でしか使えない**（グローバルで使う場合は即時実行関数を使う）。
- **Promise が解決されるまで処理が一時停止** するため、`then()` よりも直感的に書ける。

---

## **3. `async/await` の具体例**
### **① Promise チェーン（`.then()` を使う場合）**
通常の `fetch` を使った非同期処理では、`.then()` を使って結果を取得します。

```javascript
fetch("https://jsonplaceholder.typicode.com/todos/1")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```

---

### **② `async/await` を使った書き方**
同じ処理を `async/await` で書くと、よりシンプルで可読性が向上します。

```javascript
async function fetchData() {
  try {
    let response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

🔹 **メリット**
- `.then()` のネストがなくなり、**コードが読みやすい**。
- `try/catch` を使うことで、**エラーハンドリングが統一的に行える**。

---

## **4. `try/catch` を使ったエラーハンドリング**
`async/await` では、`try/catch` を使うことで、エラーハンドリングが簡単になります。

```javascript
async function fetchData() {
  try {
    let response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    
    // ステータスコードをチェック
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }

    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```
✅ **ポイント**
- `response.ok` をチェックし、HTTPエラー（404や500など）をキャッチできる。
- `try/catch` でネットワークエラーも処理できる。

---

## **5. `async/await` の応用**
### **① 複数の `await` を連続で使う**
`await` を使うと、複数の非同期処理を**直感的に順番に実行**できます。

```javascript
async function fetchMultiple() {
  let user = await fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json());
  let posts = await fetch("https://jsonplaceholder.typicode.com/posts?userId=1").then(res => res.json());

  console.log("User:", user);
  console.log("Posts:", posts);
}

fetchMultiple();
```

---

### **② `Promise.all()` と `await` の組み合わせ**
上の例だと 2 回 `await` するため、リクエストが **順番に実行** されます。  
これを **並列で実行** したい場合は、`Promise.all()` を使います。

```javascript
async function fetchParallel() {
  let [user, posts] = await Promise.all([
    fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json()),
    fetch("https://jsonplaceholder.typicode.com/posts?userId=1").then(res => res.json())
  ]);

  console.log("User:", user);
  console.log("Posts:", posts);
}

fetchParallel();
```
🔹 **メリット**
- `Promise.all()` を使うことで、**非同期処理を並列実行** し、実行時間を短縮できる。

---

## **6. `async/await` の注意点**
### **① `await` を使いすぎると並列処理が遅くなる**
以下のように `await` を使いすぎると、**リクエストが順番に実行されてしまい、パフォーマンスが低下** します。

```javascript
async function badExample() {
  let user = await fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json());
  let posts = await fetch("https://jsonplaceholder.typicode.com/posts?userId=1").then(res => res.json());

  console.log(user, posts);
}
```
✅ **改善策**
- **並列実行するなら `Promise.all()` を使う**

---

### **② `async` 関数は `await` なしでも Promise を返す**
`async` 関数の中で `await` を使わなくても、Promise を返します。

```javascript
async function test() {
  return "Hello!";
}

test().then(console.log); // "Hello!" が表示される
```

---

## **7. `async/await` のまとめ**
✅ **メリット**
- `.then()` より **シンプルで直感的に書ける**。
- `try/catch` で **エラーハンドリングが統一的に行える**。
- `Promise.all()` を使えば **並列実行も可能**。

❌ **デメリット**
- `await` を使いすぎると **並列処理ができずパフォーマンスが低下** する。
- `async` 関数は **トップレベルでは直接使えない**（`IIFE` や `.then()` が必要）。

---

## **8. 実践的なコード（Spring Boot との連携）**
最後に、`fetch` を `async/await` で使い、Java（Spring Boot）にアクセスするコードを示します。

```javascript
async function fetchUserData() {
  try {
    let response = await fetch("http://localhost:8080/api/user");
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    let user = await response.json();
    console.log("User data:", user);
  } catch (error) {
    console.error("Fetch error:", error);
  }
}

fetchUserData();
```

---

## **結論**
- **`async/await` を使うと、非同期処理が簡潔で分かりやすくなる！**
- **エラーハンドリングが `try/catch` で統一できる！**
- **並列処理には `Promise.all()` を使うと効率が良い！**
