今回は CSS-in-JS の人気ライブラリ、**Emotion** について解説します

---

## Emotionとは？

**Emotion** は、**CSSをJavaScript内で書ける**ライブラリ、いわゆる **CSS-in-JS** の一種です。

Reactアプリなどで、**スタイルをコンポーネントに埋め込んで管理できる**のが大きな特徴。

---

## Emotionの特徴まとめ

| 特徴 | 内容 |
|------|------|
|  スタイルをコンポーネントごとに管理 | SCSSのBEM問題やグローバル汚染から解放される |
|  高速 | コンパイル時に最適化され、ランタイムも軽量 |
|  2つの書き方が選べる | `styled`と`css`どちらも使える |
|  変数やpropsに応じたスタイル変更が簡単 | JavaScriptの力がそのまま使える |
|  TypeScriptとの相性も良い | 型補完が効くので快適 |

---

## インストール方法（React）

```bash
npm install @emotion/react @emotion/styled
```

---

## 基本の使い方

### styled API（コンポーネントごとにスタイルを定義）

```jsx
/** @jsxImportSource @emotion/react */
import styled from '@emotion/styled';

const Button = styled.button`
  background-color: hotpink;
  font-size: 16px;
  padding: 8px 16px;
  border-radius: 8px;
  &:hover {
    background-color: deeppink;
  }
`;

export default function App() {
  return <Button>クリック</Button>;
}
```

---

### cssプロップで1回限りのスタイル（ユーティリティ的）

```jsx
/** @jsxImportSource @emotion/react */
import { css } from '@emotion/react';

const buttonStyle = css`
  color: white;
  background-color: navy;
  padding: 10px;
  border-radius: 5px;
`;

export default function App() {
  return <button css={buttonStyle}>クリック</button>;
}
```

---

## propsでスタイルを動的に変更

```jsx
const Button = styled.button`
  background-color: ${props => (props.primary ? 'blue' : 'gray')};
  color: white;
`;

export default function App() {
  return (
    <>
      <Button>デフォルト</Button>
      <Button primary>プライマリ</Button>
    </>
  );
}
```

---

## 他のCSS-in-JSライブラリとの違い

| ライブラリ | 特徴 |
|------------|------|
| **Emotion** | 柔軟＆高速。`styled`も`css`も両方使える。 |
| **Styled Components** | 人気No.1。文法はEmotionと似てる。 |
| **JSS** | Material UIで使われてるが今は非推奨傾向。 |
| **Stitches / Vanilla Extract** | TypeScript重視・より軽量 |

---

## よく使う機能

- `@emotion/styled`：`styled.div` などでコンポーネントスタイル
- `@emotion/react`：
  - `css`関数でユーティリティ的な使い方
  - `ThemeProvider` でテーマ管理も可能
- `Global` コンポーネントでCSSのリセットなど

---

## Theme管理（共通スタイル）

```jsx
// テーマ定義
const theme = {
  colors: {
    primary: 'tomato',
    secondary: 'skyblue',
  },
};

// ThemeProviderで囲む
<ThemeProvider theme={theme}>
  <App />
</ThemeProvider>

// styled内でテーマ参照
const Box = styled.div`
  color: ${props => props.theme.colors.primary};
`;
```

---

## まとめ

> Emotionは「**ReactでスッキリとCSSを書くための最強ツールのひとつ**」です。  
> `styled-components`と似ているけど、**軽量＆柔軟で好まれる人も多い**！

