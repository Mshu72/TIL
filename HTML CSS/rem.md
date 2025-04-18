`rem` は、CSSでフォントサイズなどのレイアウトに関するプロパティを設定する際に使用される相対単位です。 `rem` は「root em」の略で、ページのルート要素（通常は `<html>`）のフォントサイズを基準にします。

### 特徴と利点

1. **ルートフォントサイズ基準**  
   - `rem` 単位は、HTMLドキュメントのルート要素（`<html>`タグ）のフォントサイズを基準に計算されます。ほとんどのブラウザの初期設定では、このルートフォントサイズが `16px` になっています。
   - 例として、ルートのフォントサイズが `16px` の場合、`1rem = 16px` になります。したがって、`2rem` であれば `32px` です。

2. **レスポンシブデザインに便利**  
   - ルートのフォントサイズを変更することで、`rem` 単位で指定した要素のサイズが一括で変更できます。これにより、ページ全体のサイズ調整が簡単になり、レスポンシブデザインに適しています。
   - たとえば、メディアクエリを使ってルートフォントサイズを変更すると、`rem` で指定された全体のフォントやレイアウトが自動で適応します。

3. **他の相対単位（`em` など）との違い**  
   - `em` 単位は親要素のフォントサイズを基準にするのに対し、`rem` は常にルート要素（`<html>`）を基準にするので、計算が容易です。
   - ネストした要素のフォントサイズ指定において `em` は継承の影響を受けるため計算が複雑になることがありますが、`rem` はルートサイズ基準で一貫性があるため、可読性が高くなります。

### 具体例

以下のようにHTMLとCSSがあるとします：

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    html {
      font-size: 16px; /* 1rem = 16px */
    }
    body {
      font-size: 1rem; /* 16px */
    }
    h1 {
      font-size: 2rem; /* 32px */
    }
    p {
      font-size: 0.875rem; /* 14px */
    }
  </style>
</head>
<body>
  <h1>Hello World</h1>
  <p>This is a paragraph.</p>
</body>
</html>
```

上記のコードで、各要素のサイズは以下のようになります：

- `<h1>` の `font-size` は `2rem` なので `32px`。
- `<p>` の `font-size` は `0.875rem` なので `14px`。

ルート要素のフォントサイズを変更すれば、`rem` で指定したすべての要素が新しいサイズに基づいて調整されます。
