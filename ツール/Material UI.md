**Material UI**（現在は **MUI** としてブランド名が変更されています）は、**React 向けの人気 UI コンポーネントライブラリ**です。

---

## Material UI（MUI）とは？

**Material UI（MUI）** は、Google のデザイン言語「[Material Design](https://m3.material.io/)」に基づいた **React コンポーネントライブラリ**です。
React アプリでプロフェッショナルで一貫性のある UI を素早く構築できます。

---

## 特徴

| 特徴                           | 説明                                            |
| ---------------------------- | --------------------------------------------- |
| Google の Material Design に準拠 | 統一された見た目と使いやすい操作性を提供                          |
| 豊富なコンポーネント群                  | ボタン、ダイアログ、テーブル、ツールバー、アイコン、フォームなどを網羅           |
| スタイリングが柔軟                    | `styled-components` や Emotion を使って柔軟にカスタマイズ可能 |
| TypeScript 対応                | 型定義が整っており、TypeScript で安心して使える                 |
| ダークモード、レスポンシブ対応              | テーマ切替や画面サイズ対応が簡単                              |
| 高いアクセシビリティ                   | ARIA 属性やキーボード操作への対応が考慮されている                   |

---

##  主なコンポーネント例

| カテゴリ    | コンポーネント例                                           |
| ------- | -------------------------------------------------- |
| 入力系     | `<TextField>`, `<Checkbox>`, `<Radio>`, `<Slider>` |
| 表示系     | `<Typography>`, `<Avatar>`, `<Badge>`              |
| レイアウト系  | `<Grid>`, `<Box>`, `<Stack>`                       |
| ナビゲーション | `<AppBar>`, `<Drawer>`, `<Tabs>`                   |
| フィードバック | `<Snackbar>`, `<Dialog>`, `<Progress>`             |
| データ表示   | `<Table>`, `<List>`, `<Card>`                      |

---

## 基本的な使い方（例）

```tsx
import * as React from 'react';
import Button from '@mui/material/Button';

export default function MyApp() {
  return <Button variant="contained" color="primary">クリック</Button>;
}
```

---

## インストール方法

```bash
# 必要なパッケージ
yarn add @mui/material @emotion/react @emotion/styled
```

（MUI は Emotion をデフォルトのスタイルエンジンにしています）

---

## 補足：バージョンの違い

* `@material-ui/*` → MUI v4 以前のパッケージ名（旧ブランド）
* `@mui/*` → MUI v5 以降のパッケージ名（現行）

---

## 公式サイト・ドキュメント

* [MUI 公式サイト](https://mui.com/)
* [コンポーネント一覧](https://mui.com/material-ui/react-button/)
* [テーマ設定](https://mui.com/material-ui/customization/theming/)

---
