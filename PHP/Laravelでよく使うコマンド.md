Laravelでよく使うコマンドとその解説を以下にまとめました。Laravelの開発で日常的によく使われるものを中心にしています。

---

##  基本系 Artisan コマンド

### `php artisan list`
- **説明**：すべてのArtisanコマンド一覧を表示します。
- **用途**：どんなコマンドがあるか調べたいとき。

---

### `php artisan help [コマンド名]`
- **例**：`php artisan help migrate`
- **説明**：指定したコマンドの詳しい説明を表示。
- **用途**：コマンドの使い方を調べたいとき。

---

##  アプリケーション開発でよく使うコマンド

### `php artisan make:controller ControllerName`
- **説明**：コントローラクラスを作成。
- **例**：`php artisan make:controller UserController`

---

### `php artisan make:model ModelName`
- **説明**：Eloquentモデルを作成。
- **例**：`php artisan make:model Post`

---

### `php artisan make:migration create_posts_table`
- **説明**：マイグレーションファイルを作成。
- **用途**：テーブルを作成・変更するスクリプトを定義。
- **例**：`php artisan make:migration add_title_to_posts_table`

---

### `php artisan migrate`
- **説明**：マイグレーションを実行してデータベース構造を変更。
- **用途**：DBにテーブルを作成・変更。

---

### `php artisan migrate:rollback`
- **説明**：直前のマイグレーションを取り消す。
- **用途**：テーブルの変更を元に戻したいとき。

---

### `php artisan db:seed`
- **説明**：シーダーを使ってテストデータを挿入。
- **用途**：開発中にダミーデータを入れる。

---

### `php artisan make:seeder SeederName`
- **説明**：シーダーファイルを作成。
- **例**：`php artisan make:seeder UsersTableSeeder`

---

### `php artisan tinker`
- **説明**：LaravelのREPL。Eloquentや関数を直接試せる。
- **用途**：簡単なデータ操作やテストに便利。

---

##  テスト関連

### `php artisan make:test TestClassName`
- **説明**：テストクラスを作成。
- **例**：`php artisan make:test UserTest`

---

### `php artisan test`
- **説明**：すべてのテストを実行。
- **用途**：コードに問題がないかチェック。

---

##  その他便利なコマンド

### `php artisan route:list`
- **説明**：定義されている全ルートを一覧表示。
- **用途**：ルーティングの確認に便利。

---

### `php artisan config:cache`
- **説明**：設定ファイルのキャッシュを再生成。
- **用途**：設定変更後の反映に必要な場合。

---

### `php artisan cache:clear`
- **説明**：キャッシュのクリア。
- **用途**：設定変更後にキャッシュを消して確認したい時。

---

### `php artisan serve`
- **説明**：ローカルサーバーを起動（通常は http://localhost:8000）。
- **用途**：開発中のアプリを簡単に確認。

