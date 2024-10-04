# !important
`!important`は、CSSルールに優先度を強制的に与えるためのキーワードです。  
通常のスタイルの継承や優先順位を無視して、そのプロパティに定義されたスタイルが必ず適用されるようにします。

```css
.button {
    color: red !important;
}
```
# 使用する際の注意点
- 過剰使用を避ける:  
 `!important`を多用すると、スタイルの管理が難しくなります。  
  複雑な優先順位の問題が発生しやすくなり、CSSのメンテナンスが難しくなるので、基本的には必要最低限に抑えるべきです。
- 優先順位:  
  同じ要素に対して複数の`!important`が使われた場合、より詳細に定義されたセレクタ（つまり、セレクタの具体性が高いもの）が優先されます。