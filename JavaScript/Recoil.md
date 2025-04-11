
##  Recoilとは？

**Recoil**は、Facebookが開発したReact向けの**状態管理ライブラリ**です。

Reactの`useState`や`useContext`を使った状態管理の限界（ネストが深くなる、再レンダリングが多くなるなど）を解消するために作られました。

特に以下のようなケースで威力を発揮します：

- グローバルに状態を共有したい
- 状態の依存関係が複雑（Aが変わるとBも変わるなど）
- コンポーネント間で状態を細かく分割・再利用したい

---

## 基本の考え方：AtomとSelector

### Atom（アトム）
- 「**状態の最小単位**」＝グローバルなuseStateのようなもの。
- どのコンポーネントからでも読み書きできる。

```js
import { atom } from 'recoil';

export const countState = atom({
  key: 'countState', // 一意なキー
  default: 0,        // 初期値
});
```

### Selector（セレクター）
- 状態から**導出された値**や**派生的な処理**を定義する。
- `useMemo`のようにキャッシュされ、必要な時だけ再計算される。

```js
import { selector } from 'recoil';
import { countState } from './atoms';

export const doubleCountState = selector({
  key: 'doubleCountState',
  get: ({ get }) => {
    const count = get(countState);
    return count * 2;
  },
});
```

---

## 実際の使い方

```jsx
import { RecoilRoot, useRecoilState, useRecoilValue } from 'recoil';
import { countState, doubleCountState } from './store';

function Counter() {
  const [count, setCount] = useRecoilState(countState);
  const doubleCount = useRecoilValue(doubleCountState);

  return (
    <div>
      <p>カウント: {count}</p>
      <p>2倍: {doubleCount}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}

function App() {
  return (
    <RecoilRoot> {/* Recoilを使うためのラッパー */}
      <Counter />
    </RecoilRoot>
  );
}
```

---

##  Recoilのメリット

| 特徴 | 説明 |
|------|------|
|  Reactと密接に連携 | フックベースでReactに自然に馴染む |
|  状態を分割管理 | コンポーネント単位で管理しやすい |
|  依存関係の自動管理 | セレクターが自動で依存関係を追ってくれる |
|  部分的な再レンダリング | 無駄な再描画が起こらない |
|  SSR対応（部分的に） | Next.jsとも併用可能（工夫は必要） |

---

## 注意点

- React公式の状態管理ではない（けどFacebook製）
- 学習コストはReduxより低いが、セレクターや非同期処理を使いこなすには慣れが必要
- 大規模開発での導入実績はReduxほど多くない（が、増えてきている）

---

## まとめ

> Recoilは「**Reactらしい書き方で、柔軟に状態管理したい**」人にとって、かなり使いやすいライブラリです。
