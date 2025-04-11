Next.jsは、**React**をベースにしたオープンソースのフレームワークで、**Vercel**によって開発・保守されています。ReactでWebアプリケーションを構築する際に、より効率的かつスケーラブルな方法を提供します。Next.jsを使用することで、**サーバーサイドレンダリング（SSR）**や**静的サイト生成（SSG）**を簡単に実装でき、SEO対策やパフォーマンス向上を図ることができます。

---

###  **Next.jsの主な特徴**  
1. **サーバーサイドレンダリング（SSR）**  
   - リクエスト時にサーバー上でページをレンダリング。  
   - SEOに強く、動的コンテンツに適しています。

2. **静的サイト生成（SSG）**  
   - ビルド時にHTMLを生成し、パフォーマンスとスケーラビリティが向上。  
   - ブログやドキュメントサイトに最適。

3. **クライアントサイドレンダリング（CSR）**  
   - ブラウザ上でページをレンダリング。  
   - 動的なインタラクションが多いページで有効。

4. **API Routes**  
   - Next.js内でAPIエンドポイントを作成できるため、バックエンド機能もシームレスに実装可能。

5. **画像最適化（`next/image`）**  
   - 自動的に画像を最適化し、パフォーマンスを向上。

6. **ファイルベースのルーティング**  
   - `pages`ディレクトリにファイルを作成するだけで、自動的にルーティングが設定。

7. **インクリメンタルスタティックリジェネレーション（ISR）**  
   - 静的ページを必要に応じて再生成し、パフォーマンスと動的なデータ更新のバランスを実現。

8. **TypeScriptサポート**  
   - TypeScriptが組み込みでサポートされており、型安全な開発が可能。

---

###  **Next.jsのインストール方法**  
```bash
npx create-next-app@latest my-next-app
# または
yarn create next-app my-next-app
```

その後、以下のコマンドで開発サーバーを起動します：
```bash
cd my-next-app
npm run dev
```
ブラウザで `http://localhost:3000` にアクセスすると、Next.jsアプリが動作していることを確認できます。

---

###  **Next.jsが適しているユースケース**  
- SEOが重要なブログやEコマースサイト  
- 高速なパフォーマンスが求められるWebアプリケーション  
- 動的なデータを必要とするダッシュボードやアプリ  
- 静的コンテンツをホスティングするマーケティングページ  

---

###  **Next.jsのメリット**  
- SEO最適化が簡単  
- パフォーマンスが高い  
- 開発者体験が向上（ホットリロード、優れたドキュメントなど）  
- Vercelとシームレスなデプロイ  

---

**Next.js**は、**Reactベースのフレームワーク**で、以下のような特徴を持っています：

| 特徴 | 説明 |
|------|------|
|  サーバーサイドレンダリング（SSR） | SEOや初期表示に強い |
|  静的サイト生成（SSG） | 高速・キャッシュしやすい |
|  ルーティングが超簡単 | `pages/`フォルダの構成だけでルーティングできる |
|  APIルートも使える | バックエンドいらずでAPI作れる |
|  TypeScriptやTailwindとの相性も◎ | セットアップが簡単 |
|  App Router（新機能）対応 | レイアウトやローディングUIの設計が超柔軟に |

---

## ディレクトリ構成（基本）

```
my-next-app/
├── pages/          ← ページルーティング（例: /about は pages/about.js）
│   └── index.js    ← ルートページ (/)
├── public/         ← 画像や静的ファイル
├── styles/         ← CSSやSCSS
├── components/     ← Reactコンポーネント
├── next.config.js  ← 設定ファイル
└── package.json
```

※ `app/`ディレクトリを使う「App Router」という新ルーティング方式もあります（後述）

---

## ルーティングはフォルダで完結！

```jsx
// pages/about.js
export default function About() {
  return <h1>このページは About です</h1>;
}
```

このだけで `/about` ページが完成！ルーティングの設定不要✨

---

## データ取得方法

Next.jsでは「どこでデータを取るか？」で処理が変わります。

### ページを表示する時にデータを取る：

#### SSG（Static Site Generation）

```js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return { props: { data } };
}
```

#### SSR（Server Side Rendering）

```js
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return { props: { data } };
}
```

---

## APIルートも作れる！

```js
// pages/api/hello.js

export default function handler(req, res) {
  res.status(200).json({ message: 'こんにちは Next.js API！' });
}
```

このコードだけで `/api/hello` というAPIエンドポイントが動く🎉

---

## App Routerとは？

Next.js 13以降では `app/` ディレクトリを使った**App Router**が登場しました。

特徴：
- `layout.tsx` による共通レイアウト管理
- `loading.tsx` でローディングUIを作れる
- `server component` と `client component` の使い分けが可能（パフォーマンス向上）

```tsx
// app/page.tsx
export default function Home() {
  return <h1>ホームページ</h1>;
}

// app/layout.tsx
export default function Layout({ children }) {
  return (
    <html>
      <body>
        <header>ヘッダー</header>
        {children}
        <footer>フッター</footer>
      </body>
    </html>
  );
}
```

---

## Next.jsが向いている用途

- ブログやマーケティングサイト（SEOに強い）
- 管理画面やダッシュボード（SSR + APIで構成できる）
- フルスタックアプリ（フロントもバックエンドも1つのコードで）

---

## 便利な機能まとめ

| 機能 | 説明 |
|------|------|
| Image最適化 | `<Image>`コンポーネントで自動圧縮・遅延読み込み |
| Link最適化 | `<Link>`タグでクライアント遷移が高速 |
| Middleware | リクエストを途中で処理（認証チェックなど） |
| インクリメンタル再生成 | 一部ページだけSSGを再生成（更新速い） |

---

## まとめ

Next.jsは「**Reactの上位互換 + サーバー機能 + 静的サイトビルド**」のハイブリッド！

> 「Reactで作るならNext.js使っとけば安心」ってレベルで便利です。

