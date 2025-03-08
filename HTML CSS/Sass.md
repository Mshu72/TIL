### SASS（Syntactically Awesome Stylesheets）とは？

SASSは、CSSをより効率的に記述するための**CSSメタ言語**（プリプロセッサ）の一つです。CSSを拡張し、**変数・ネスト・ミックスイン・継承**などの機能を提供することで、より柔軟で保守しやすいスタイルを作成できます。

---

## **SASSの主な特徴**

### 1. **変数（Variables）**
SASSでは、CSS内で変数を使用できるため、**同じ値を何度も記述する手間を省ける**上に、**一括変更**も簡単になります。

```scss
$primary-color: #3498db;

body {
  background-color: $primary-color;
  color: white;
}
```

### 2. **ネスト（Nesting）**
CSSの構造をそのままネストできるので、**可読性が向上**します。

```scss
nav {
  ul {
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    text-decoration: none;
    color: blue;
  }
}
```

### 3. **ミックスイン（Mixins）**
繰り返し使うスタイルをミックスインとして定義し、**コードの再利用が可能**になります。

```scss
@mixin button-style {
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}

button {
  @include button-style;
}
```

### 4. **継承（Inheritance）**
既存のスタイルを継承し、**DRY（Don't Repeat Yourself）の原則**に基づいたコーディングができます。

```scss
%base-style {
  font-size: 16px;
  color: #333;
}

p {
  @extend %base-style;
}

span {
  @extend %base-style;
  font-weight: bold;
}
```

### 5. **演算（Operators）**
SASSでは、**計算式（+、-、*、/、%）**を使用できます。

```scss
$base-size: 16px;

h1 {
  font-size: $base-size * 2; // 32px
}
```

---

## **SASSとSCSSの違い**
SASSには2つの記法があります。

| 記法 | 特徴 |
|------|------|
| **SASS** | インデントを使い、波括弧 `{}` やセミコロン `;` を不要にするシンプルな記法 |
| **SCSS** | CSSに近い記法で、波括弧 `{}` やセミコロン `;` を使う（現在の主流） |

#### **SASS（インデント記法）**
```sass
$primary-color: #3498db

body
  background-color: $primary-color
  color: white
```

#### **SCSS（CSSライクな記法）**
```scss
$primary-color: #3498db;

body {
  background-color: $primary-color;
  color: white;
}
```

**現在はSCSSの方が主流**なので、基本的にSCSSを使うことをおすすめします。

---

## **SASSの導入方法**
SASSを使用するには、以下の方法があります。

### 1. **Node.js環境でSASSをインストール**
```sh
npm install -g sass
```

### 2. **SASSファイル（.scss）をCSSにコンパイル**
```sh
sass input.scss output.css
```

### 3. **自動コンパイル（watchモード）**
```sh
sass --watch input.scss:output.css
```

---

## **まとめ**
 - SASSはCSSを拡張するプリプロセッサ  
 - 変数、ネスト、ミックスイン、継承などで**保守性が向上**  
 - **SCSS記法が主流**で、CSSに近い書き方  
 - コマンドでSASSを**CSSにコンパイル**できる  
