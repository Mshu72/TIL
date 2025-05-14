Reactのアプリケーションで画面遷移を行うには、\*\*`React Router`\*\*というライブラリを使います。以下に基本的な使い方を説明します。

---

## 1. ライブラリのインストール

まず、React Router をインストールします：

```bash
npm install react-router-dom
```

または

```bash
yarn add react-router-dom
```

---

## 2. ルーティングの基本構成

React Router v6 以降を使う場合、以下のように構成します。

### `App.tsx` または `App.jsx`

```tsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

## 3. ページコンポーネントを作成

### `Home.tsx`

```tsx
import { Link } from 'react-router-dom';

function Home() {
  return (
    <div>
      <h1>ホームページ</h1>
      <Link to="/about">Aboutページへ移動</Link>
    </div>
  );
}

export default Home;
```

### `About.tsx`

```tsx
function About() {
  return (
    <div>
      <h1>Aboutページ</h1>
    </div>
  );
}

export default About;
```

---

## 4. `useNavigate` でプログラム的に遷移

画面遷移をコードで制御したい場合は `useNavigate()` を使用します：

```tsx
import { useNavigate } from 'react-router-dom';

function Home() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/about');
  };

  return (
    <div>
      <button onClick={handleClick}>Aboutページへ</button>
    </div>
  );
}
```

---

## よくある用途

* 認証後に `/dashboard` に遷移させる
* フォーム送信後に別の画面に移動させる
* リンククリックでページを切り替える

---
