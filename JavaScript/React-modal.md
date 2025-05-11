`react-modal` は、React アプリケーションでモーダル（ダイアログ）を簡単に実装できる軽量ライブラリです。アクセシビリティ対応（ARIA属性やフォーカス制御）にも優れており、多くのプロジェクトで利用されています。

---

## 1. インストール

```bash
npm install react-modal
# または
yarn add react-modal
```

---

## 2. 基本的な使い方

### App.js の例

```jsx
import React, { useState } from 'react';
import Modal from 'react-modal';

// ルートエレメントの指定（必須）
Modal.setAppElement('#root');

function App() {
  const [modalIsOpen, setModalIsOpen] = useState(false);

  return (
    <div>
      <h2>React Modal の基本例</h2>
      <button onClick={() => setModalIsOpen(true)}>モーダルを開く</button>

      <Modal
        isOpen={modalIsOpen}
        onRequestClose={() => setModalIsOpen(false)} // 背景クリックやEscキーで閉じる
        contentLabel="Example Modal"
      >
        <h3>モーダルの中身</h3>
        <p>これは react-modal の例です。</p>
        <button onClick={() => setModalIsOpen(false)}>閉じる</button>
      </Modal>
    </div>
  );
}
```

---

## 3. スタイルのカスタマイズ

`style` オプションでカスタム CSS を直接指定できます。

```jsx
<Modal
  isOpen={modalIsOpen}
  onRequestClose={() => setModalIsOpen(false)}
  style={{
    content: {
      top: '50%',
      left: '50%',
      right: 'auto',
      bottom: 'auto',
      marginRight: '-50%',
      transform: 'translate(-50%, -50%)'
    },
    overlay: {
      backgroundColor: 'rgba(0, 0, 0, 0.5)'
    }
  }}
>
```

---

## 4. アクセシビリティ対応

* `Modal.setAppElement('#root')` は必須。スクリーンリーダーのために、モーダル以外のコンテンツを非表示にします。
* `onRequestClose` を使って ESCキーや背景クリック時の閉じる処理を指定。

---

## 5. よく使う Props

| Prop                        | 説明                         |
| --------------------------- | -------------------------- |
| `isOpen`                    | モーダルを表示するかどうか              |
| `onRequestClose`            | モーダル外クリックや ESC で呼ばれるコールバック |
| `style`                     | モーダルとオーバーレイのスタイルを指定        |
| `contentLabel`              | アクセシビリティ用の説明               |
| `shouldCloseOnOverlayClick` | オーバーレイのクリックで閉じる（デフォルトtrue） |
| `shouldCloseOnEsc`          | ESCで閉じる（デフォルトtrue）         |

