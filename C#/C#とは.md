 **C#（シーシャープ）** について解説します。

---

##  C#とは？

**C#（シーシャープ）** は、Microsoftが開発した**オブジェクト指向型のプログラミング言語**です。

* 読み方：シーシャープ（"C++" より高機能という意味を込めた名前）
* 誕生：2000年、.NETフレームワークとともに登場
* 目的：**モダンで安全性が高く、扱いやすい言語**を目指して設計されました。

---

##  特徴

| 特徴                                    | 説明                                         |
| ------------------------------------- | ------------------------------------------ |
|  **オブジェクト指向**                        | Javaに似たクラスベース設計。継承、カプセル化、ポリモーフィズムが使えます。    |
|  **安全なメモリ管理**                        | C++と違い、\*\*ガベージコレクション（自動的なメモリ解放）\*\*を持ちます。 |
|  **Visual Studioとの連携**               | Microsoft製IDE「Visual Studio」で効率よく開発できます。   |
|  **マルチプラットフォーム（.NET Core/.NET 5以降）** | Windowsだけでなく、Mac、Linuxでも動作可能になりました。        |
|  **ゲーム開発にも強い**                       | \*\*Unity（ユニティ）\*\*というゲームエンジンがC#を使っています。   |

---

## 主な使用例

* **Windowsデスクトップアプリ**（WPF、WinForms）
* **Webアプリケーション**（ASP.NET）
* **ゲーム開発**（Unity）
* **クラウドアプリケーション**（Azure）
* **モバイルアプリ**（Xamarin）

---

## C#のサンプルコード

### Hello World（基本構文）

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, world!");
    }
}
```

### クラスとメソッド

```csharp
public class Person
{
    public string Name { get; set; }

    public void SayHello()
    {
        Console.WriteLine($"こんにちは、私は {Name} です。");
    }
}
```

---

## C#の実行環境

| 名前                      | 説明                                   |
| ----------------------- | ------------------------------------ |
| **.NET Framework**      | 古くからあるWindows専用の実行環境                 |
| **.NET Core / .NET 5+** | 最新のクロスプラットフォーム対応ランタイム                |
| **Mono**                | 主にLinux・Mac用のオープンソース実装（Unityの裏側でも使用） |

---

## C#を学ぶのに向いている人

* **Windowsアプリを作りたい**
* **ゲーム開発（Unity）をしたい**
* **WebアプリやAPIを効率よく開発したい**
* **Visual Studioなどのツールを使いたい**

---

## まとめ

| 項目    | C#のポイント                               |
| ----- | ------------------------------------- |
| 開発元   | Microsoft                             |
| メモリ管理 | 自動（ガベージコレクション）                        |
| 主な用途  | Windowsアプリ、ゲーム、Web API                |
| 実行環境  | .NET 5/6/7 など                         |
| 開発ツール | Visual Studio / Visual Studio Code など |


