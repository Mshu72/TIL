Springには、フォーム入力やオブジェクトのプロパティのバリデーションをサポートするための便利なバリデーションアノテーションが豊富に用意されています。これらのアノテーションは、Bean Validation（JSR 380）をベースにしており、`javax.validation`や`org.hibernate.validator`から提供されるアノテーションを使用することで簡単に入力チェックが可能です。

### よく使われるバリデーションアノテーション

#### 1. `@NotNull`
- **説明**: フィールドが`null`でないことをチェックします。
- **例**:
  ```java
  @NotNull(message = "このフィールドは必須です")
  private String name;
  ```

#### 2. `@NotEmpty`
- **説明**: 文字列やコレクションが空でないことをチェックします（`null`も空として扱います）。
- **例**:
  ```java
  @NotEmpty(message = "名前は空にできません")
  private String name;
  ```

#### 3. `@NotBlank`
- **説明**: 文字列が空白でないことをチェックします（空文字やスペースのみも不可）。
- **例**:
  ```java
  @NotBlank(message = "名前には空白以外の文字を含めてください")
  private String name;
  ```

#### 4. `@Size`
- **説明**: 文字列やコレクションのサイズが指定された範囲内であることをチェックします。
- **例**:
  ```java
  @Size(min = 2, max = 20, message = "名前は2文字以上20文字以下にしてください")
  private String name;
  ```

#### 5. `@Min` / `@Max`
- **説明**: 数値の最小値・最大値を制限します。
- **例**:
  ```java
  @Min(value = 18, message = "年齢は18以上である必要があります")
  @Max(value = 100, message = "年齢は100以下である必要があります")
  private int age;
  ```

#### 6. `@Email`
- **説明**: メールアドレスの形式をチェックします。
- **例**:
  ```java
  @Email(message = "有効なメールアドレスを入力してください")
  private String email;
  ```

#### 7. `@Pattern`
- **説明**: 正規表現パターンに一致するかどうかをチェックします。
- **例**:
  ```java
  @Pattern(regexp = "^[a-zA-Z0-9]+$", message = "ユーザー名には英数字のみ使用可能です")
  private String username;
  ```

#### 8. `@Positive` / `@PositiveOrZero`
- **説明**: 正の数かどうかをチェックします（または0以上）。
- **例**:
  ```java
  @Positive(message = "価格は正の数である必要があります")
  private int price;
  ```

#### 9. `@Negative` / `@NegativeOrZero`
- **説明**: 負の数かどうかをチェックします（または0以下）。
- **例**:
  ```java
  @Negative(message = "値は負の数である必要があります")
  private int negativeValue;
  ```

#### 10. `@Future` / `@FutureOrPresent`
- **説明**: 日付が未来の日付であること（または現在）をチェックします。例えば、予約日などのチェックに使用します。
- **例**:
  ```java
  @Future(message = "予約日は未来の日付を指定してください")
  private LocalDate reservationDate;
  ```

#### 11. `@Past` / `@PastOrPresent`
- **説明**: 日付が過去の日付であること（または現在）をチェックします。例えば、誕生日のチェックに使用します。
- **例**:
  ```java
  @Past(message = "生年月日は過去の日付である必要があります")
  private LocalDate birthDate;
  ```

### カスタムメッセージとグループの使用
- **カスタムメッセージ**: 各アノテーションの`message`属性でエラーメッセージをカスタマイズできます。
- **グループ**: 例えば、`@Validated(Group.class)`を指定すると特定のバリデーションアノテーションを実行するグループ分けが可能です。これにより、場面に応じた柔軟なバリデーションが行えます。

### バリデーションの使用方法
Springでは、リクエストボディやコントローラメソッドの引数にバリデーションを適用するため、`@Valid`や`@Validated`を使用します。

```java
@PostMapping("/register")
public ResponseEntity<String> registerUser(@Valid @RequestBody UserDto user) {
    // ユーザー登録の処理
    return ResponseEntity.ok("ユーザー登録が成功しました");
}
```

これらのバリデーションアノテーションを適切に利用することで、データの品質を確保し、エラーの早期検出が可能になります。
