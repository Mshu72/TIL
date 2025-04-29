
# Ruby on Railsとは？

**Ruby on Rails（ルビー・オン・レイルズ）** は、  
**Ruby** 言語で書かれた **Webアプリケーションフレームワーク** です。  
略してよく **Rails** と呼ばれます。

Railsは、アプリケーション開発を「速く」「シンプルに」「楽しく」することを目指して設計されています。  
2004年、**David Heinemeier Hansson（DHH）** によって開発されました。

---

## Ruby on Railsの特徴

| 特徴                  | 説明                                                                 |
|----------------------|--------------------------------------------------------------------|
| **MVCアーキテクチャ**    | アプリを「モデル(Model)」「ビュー(View)」「コントローラー(Controller)」に分けて構成します。 |
| **DRY原則**           | "Don't Repeat Yourself"（繰り返しを避ける）。コードの重複を防ぎます。             |
| **CoC原則**           | "Convention over Configuration"（設定より規約）。標準的なルールを守れば、設定不要。  |
| **Scaffold機能**      | 簡単なコマンドでCRUD（作成・読み取り・更新・削除）画面を自動生成できます。         |
| **豊富なジェム(Gem)**  | 外部ライブラリ（Gem）を使って機能追加が簡単です。                                  |
| **ActiveRecord**      | データベースと簡単にやりとりできるORM(Object Relational Mapping)を提供します。    |

---

## Railsの構成イメージ（MVC）

```
ブラウザ
  ↓（リクエスト）
ルーティング (routes.rb)
  ↓
コントローラー (Controller)
  ↓
モデル (Model) ←→ データベース (DB)
  ↓
ビュー (View)
  ↓（HTML生成）
ブラウザ
```

- **Model**：データを管理（例：ユーザ情報）
- **View**：画面を表示（例：ユーザ一覧画面）
- **Controller**：リクエストを受け取り、モデルとビューをつなぐ（例：ユーザ一覧を取得して表示する）

---

## よくある開発の流れ

1. **Railsプロジェクト作成**  
   ```bash
   rails new myapp
   ```

2. **モデル作成**  
   ```bash
   rails generate model User name:string email:string
   ```

3. **データベースにテーブル作成**  
   ```bash
   rails db:migrate
   ```

4. **コントローラー作成**  
   ```bash
   rails generate controller Users
   ```

5. **ビュー作成**  
   HTML＋Rubyで書くテンプレートファイル（`erb`ファイル）を作る。

6. **ルーティング設定**  
   `config/routes.rb` にURLとコントローラーの対応を書く。

7. **サーバ起動**  
   ```bash
   rails server
   ```
   → `http://localhost:3000` でアプリを見れる！

---

## Ruby on Railsのメリット・デメリット

### メリット
- Webアプリのプロトタイプを高速で作れる
- コードがスッキリ読みやすい
- 世界中で使われている → 情報も多い
- 学習コストが比較的低い（特に初期開発が楽）

### デメリット
- 自由度が少ない（規約に縛られる）
- 大規模アプリではパフォーマンスチューニングが必要になる
- Ruby自体が他の言語（例：Go、Rust）より遅いことがある

