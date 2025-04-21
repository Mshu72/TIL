**Kotlin（コットリン）**は、**モダンで安全性の高いプログラミング言語**で、主に **Androidアプリ開発** で使われています。

---

## Kotlin（コットリン）とは？

- **JetBrains**社が開発したプログラミング言語（IntelliJ IDEAの会社）
- 2017年、**GoogleがAndroid公式言語として採用**
- Javaと完全互換があり、**Javaの代替**として注目
- 文法が簡潔でエラーが少なく、安全性が高い

---

## 主な特徴

| 特徴 | 説明 |
|------|------|
| **Javaと100%互換** | 既存のJavaライブラリをそのまま使える |
| **簡潔な文法** | Javaに比べてコード量が少ない |
| **Null安全** | NullPointerExceptionのリスクを減らす設計 |
| **関数型プログラミング対応** | ラムダ式やコレクション操作が強力 |
| **マルチプラットフォーム** | Kotlin Multiplatformでモバイル、Web、サーバー開発に対応 |

---

## Kotlinのコード例（Hello World）

```kotlin
fun main() {
    println("Hello, Kotlin!")
}
```

---

##  KotlinとJavaの比較（変数定義）

### Javaの場合
```java
String name = "Taro";
```

### Kotlinの場合
```kotlin
val name = "Taro"  // 型推論で自動的にStringになる
```

---

## Null安全の仕組み

Kotlinでは、**nullを許容する型**と**許容しない型**を分けて扱うことで、エラーを未然に防ぎます。

```kotlin
var name: String = "Taro"     // nullは入れられない
var nickname: String? = null  // ? をつけると null を許容する
```

---

## Kotlinの用途

| 分野 | 内容 |
|------|------|
| Androidアプリ開発 | Google公式サポートあり。Javaより主流になりつつある |
| サーバーサイド | Spring Boot などのフレームワークと併用可能 |
| Webフロントエンド | Kotlin/JSでJavaScriptに変換して使える |
| マルチプラットフォーム | Kotlin MultiplatformでiOS/Android両対応コードを共通化 |

---

## Kotlinを使った開発が向いている人

- Javaの冗長な文法に不満を持っている人
- Androidアプリを最新の技術で効率よく開発したい人
- 型安全でミスの少ないコードを書きたい人

