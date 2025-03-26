Thymeleaf の `th:each` は、**コレクションや配列などの複数データをループ処理（繰り返し）して HTML を動的に生成するための属性**です。   
Java の `for-each` に相当します。

---

##  `th:each` の基本構文

```html
<tr th:each="item : ${itemList}">
    <td th:text="${item.name}">名前</td>
</tr>
```

- `item`：ループ内で使う変数名（自由に名前をつけてOK）
- `itemList`：コントローラから渡されたリスト（モデルの属性）

---

##  使用例（Java → Thymeleaf）

###  コントローラ（Java）

```java
List<User> users = userService.getAllUsers();
model.addAttribute("users", users);
```

###  HTML（Thymeleaf）

```html
<table>
  <tr>
    <th>名前</th>
    <th>年齢</th>
  </tr>
  <tr th:each="user : ${users}">
    <td th:text="${user.name}">山田 太郎</td>
    <td th:text="${user.age}">25</td>
  </tr>
</table>
```

---

##  インデックス（ループの番号）を使いたいとき

```html
<tr th:each="user, stat : ${users}">
  <td th:text="${stat.index + 1}">1</td> <!-- 0始まり -->
  <td th:text="${user.name}">名前</td>
</tr>
```

| `stat.index` | 0から始まるインデックス |
|--------------|--------------------------|
| `stat.count` | 1から始まるカウント      |
| `stat.size`  | 全体のサイズ             |
| `stat.first` | 最初の要素なら true       |
| `stat.last`  | 最後の要素なら true       |

---

##  条件付きでループしたいとき

```html
<tr th:each="user : ${users}" th:if="${user.age} >= 20">
  <td th:text="${user.name}"></td>
</tr>
```

---

##  よくある使い方まとめ

| 用途             | 書き方                                 |
|------------------|----------------------------------------|
| 通常のループ      | `th:each="item : ${list}"`             |
| インデックス付き | `th:each="item, stat : ${list}"`       |
| 空チェック       | コントローラ側で null/empty チェック推奨 |
| 条件付きループ    | `th:if` や `th:unless` を併用         |

---

Thymeleaf の `th:each` を使いこなすと、画面表示をかなり柔軟に制御できます。繰り返しのデータ表示や条件付き表示など、UIの自動生成には欠かせない機能です！

