# setTimeout 
JavaScript の関数で、指定した時間が経過した後に一度だけ関数を実行するためのタイマーを設定します。  
非同期処理に利用され、一定時間後に何かしらの処理を実行したいときに便利です。

## 基本的な使い方
``javascript
setTimeout(function, delay);
```
`function`：遅延後に実行したい関数や処理。
`delay`：遅延させる時間をミリ秒単位（1秒＝1000ミリ秒）で指定します。

例えば、2秒後にメッセージを表示する場合：

```javascript
setTimeout(function() {
  console.log("2秒後に表示されるメッセージ");
}, 2000);
```
この例では、2秒（2000ミリ秒）後に console.log が実行され、メッセージが表示されます。

### 引数を渡す場合
`setTimeout` に渡す関数に引数を渡すこともできます。  
その際、次のように記述します：

```javascript
setTimeout(function(param) {
  console.log(param);
}, 2000, "Hello, World!");
```
この例では、2秒後に Hello, World! が表示されます。

## setTimeout のキャンセル
`setTimeout` は、返り値としてタイマーIDを返します。  
このIDを使って、タイマーをキャンセルすることができます。  
キャンセルには `clearTimeout`を使用します。

```javascript
let timerId = setTimeout(function() {
  console.log("実行されないはずのメッセージ");
}, 5000);

clearTimeout(timerId); // タイマーをキャンセル
```
この場合、タイマーがキャンセルされるので、メッセージは表示されません。

## setTimeout の特徴
非同期処理の一種で、指定された関数がすぐに実行されるわけではなく、JavaScript の実行コンテキストの「タスクキュー」に追加され、タイミングが来たら実行されます。  
実際の遅延時間は、システムの状況（CPUの負荷など）により若干遅れることがあります。  

このように、`setTimeout`は時間に応じた処理を遅らせたり、一度だけ実行したいタスクを指定したりする際に便利なツールです。
