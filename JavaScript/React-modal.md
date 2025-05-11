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

| props名	| 引数の型	| 説明 |   
| --- | --- | --- |   
| isOpen | Boolean | モーダルが開いているか閉じているか |   
| onAfterOpen	| Function | モーダルが開かれたあとに指定された関数が実行される |   
| onAfterClose | Function	| モーダルが閉じられたあとに指定された関数が実行される |   
| onRequestClose | Function | モーダルを閉じる命令が呼ばれた際に指定した関数が実行される |   
| closeTimeoutMS | Number | 閉じる前に待機するミリ秒 |   
| style	| {overlay: {}, content: {}} | style(CSS)を指定します。overlay(モーダルの外側の要素)とcontent(モーダルの要素)のstyleを指定する必要があります |   
| overlayClassName | String	| 指定したclassを、モーダルの外側の要素に付与します |   
| id | String	| 指定したidを、生成されるdiv要素に付与します |   
| className	| String | 指定したclassを、生成されるモーダルに付与します |   
| shouldFocusAfterRender | Boolean | モーダルが表示されたあとにフォーカスするかどうか (デフォルトがtrueなので無効にしたい場合使用する) |   
| shouldCloseOnOverlayClick	| Boolean | 外側の余白をクリックした際にモーダルを閉じる命令をだすかどうか (デフォルトがtrueなので無効にしたい場合使用する) |   
| shouldCloseOnEsc | Boolean | Escキーでモーダルを閉じるかどうか (デフォルトがtrueなので無効にしたい場合使用する) |   

その他	-	ほかにも使用できるpropsがあります。限定的な場面でしか使用しないものもあるので説明は割愛します。こちらで他のpropsを確認できます。
