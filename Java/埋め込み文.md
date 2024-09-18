# Javaにおける埋め込み分の書き方
## 1. String.format()メソッド
Javaでは、String.format()メソッドを使って変数を文字列に埋め込むことができます。%sや%dなどのフォーマット指定子を使い、Pythonのf-stringsに似た書き方が可能です。

例：
```
String name = "Alice";
int age = 25;

String message = String.format("My name is %s and I am %d years old.", name, age);
System.out.println(message);
```

このコードは以下の出力をします：

```
My name is Alice and I am 25 years old.
```

- %sは文字列のフォーマット指定子です。
- %dは整数のフォーマット指定子です。

## 2. printf()メソッド
JavaのSystem.out.printf()メソッドもString.format()と同じフォーマット指定を使って、変数を文字列に埋め込むことができます。こちらは直接コンソールに出力するため、printf()メソッド内でフォーマットと変数を指定します。

例：
```
String name = "Bob";
int age = 30;

System.out.printf("My name is %s and I am %d years old.%n", name, age);
```

このコードは以下の出力をします：

```
My name is Bob and I am 30 years old.
```

- %nは改行を挿入する指定子です。
## 3. StringBuilderまたはStringBufferを使う
StringBuilderやStringBufferを使って、文字列を結合することもできます。これは可変な文字列を扱いたい場合に便利です。

例：
```
String name = "Charlie";
int age = 28;

StringBuilder sb = new StringBuilder();
sb.append("My name is ").append(name).append(" and I am ").append(age).append(" years old.");
System.out.println(sb.toString());
``` 

このコードも以下の出力をします：

```
My name is Charlie and I am 28 years old.
```
