**Dart（ダート）**は、Googleが開発したプログラミング言語で、特に **Flutter** の開発言語として有名です。

---

## Dartとは？

- **Googleが開発したオープンソースの言語**
- Flutter（モバイル/Web/デスクトップUI開発）で使用されている
- JavaScriptの代替として設計され、**Webクライアント/モバイル/サーバー**などで使える
- コンパイル言語でもあり、**高速に動作**し、**型安全**である

---

## Dartの主な特徴

| 特徴 | 説明 |
|------|------|
| **シンプルで直感的な文法** | Java/C系言語に近く、初心者にも学びやすい |
| **静的型付け** | 明確な型システムにより、開発中に多くのエラーを防げる |
| **AOTとJITの両対応** | 実行時の速度と開発時の柔軟さを両立 |
| **非同期処理が簡単** | `async/await` による簡潔な非同期コード |
| **オブジェクト指向** | クラスベース、継承・インターフェースあり |
| **Web用にも変換可** | Dart→JavaScriptに変換してWebブラウザ上でも動作可能 |

---

## Dartのコード例（Hello World）

```dart
void main() {
  print('Hello, Dart!');
}
```

---

## 変数の定義

```dart
var name = 'Taro';      // 型推論されてString
String greeting = 'Hi'; // 明示的な型定義
final age = 30;         // 一度だけ代入可能（再代入不可）
const pi = 3.14;        // コンパイル時に決まる定数
```

---

## 関数の定義

```dart
int add(int a, int b) {
  return a + b;
}

// アロー関数（短縮形）
int multiply(int a, int b) => a * b;
```

---

## クラスの定義

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  void greet() {
    print('Hello, my name is $name and I am $age years old.');
  }
}
```

---

## 非同期処理の例

```dart
Future<void> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  print('データ取得完了');
}
```

---

## Dartの主な用途

| 分野 | 用途 |
|------|------|
| **モバイルアプリ** | FlutterでAndroid/iOS両対応アプリを開発 |
| **Webアプリ** | Dart → JavaScriptに変換してWeb対応（DartPadなど） |
| **デスクトップアプリ** | Flutter Desktop（Windows/macOS/Linux） |
| **サーバーサイド** | Dart単体でもWebサーバーやAPIが書ける（dart:io, shelfなど） |

---

## Flutterとの関係

- Flutterでアプリを書くには**Dartが必須**
- UI構築・状態管理・ルーティングなども**全てDartで記述**
- Dartの非同期処理やクラス設計が、Flutterの設計と非常にマッチしている

---

## Dartを学ぶと良い人

- Flutterでアプリを作りたい人
- シンプルでモダンな言語を使いたい人
- JavaScriptよりも型安全な言語を探している人

---
