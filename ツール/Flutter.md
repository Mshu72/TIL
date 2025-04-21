**Flutter（フラッター）**は、Googleが開発した**オープンソースのUI開発フレームワーク**です。以下のような特徴があります。

---

## Flutter（フラッター）とは？

- **モバイル・Web・デスクトップアプリ**を**単一のコードベース**で開発できるフレームワーク
- 開発言語は **Dart（ダート）**
- Google製で、**Android/iOS両対応**のアプリを効率よく作れる
- 高速な開発と、ネイティブ並みのパフォーマンスを目指している

---

## Flutter の主な特徴

| 特徴 | 説明 |
|------|------|
| **クロスプラットフォーム開発** | Android、iOS、Web、Windows、macOS、Linux用のアプリを一つのコードで開発可能 |
| **高速なホットリロード** | コード変更後、アプリを再起動せずに即反映できる（デバッグ効率アップ） |
| **豊富なウィジェット** | Material DesignやCupertinoスタイルなど、モダンなUI部品が多数用意されている |
| **Dart言語を使用** | シンプルで高速なGoogle製言語。JavaやJavaScriptに似ている |
| **高パフォーマンス** | UIをネイティブコードにコンパイルするため、滑らかに動作 |

---

## Flutter でできること

- スマホアプリ（Android / iOS）
- Webアプリ（ブラウザで動作）
- デスクトップアプリ（Windows / macOS / Linux）
- 埋め込みアプリ（IoTや自動車などのOS上）

---

## Flutter の画面構築例（コード）

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text("Flutter App")),
        body: Center(child: Text("Hello Flutter!")),
      ),
    );
  }
}
```

---

## よく使われる場面

- スタートアップ企業のモバイルアプリ開発
- プロトタイプ作成
- Webとモバイルの共通UI実装
- 大手企業のマルチプラットフォーム対応（例: Google Ads アプリ）

---

もし、Flutterを始めたいと思ったら、以下のセットアップが必要です：

- Dart SDK（Flutterに含まれてます）
- Android Studio または Visual Studio Code
- エミュレーター（Android/iOS）または実機

---
