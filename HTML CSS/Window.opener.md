`window.opener` は JavaScript で使われるプロパティで、現在のウィンドウ (またはタブ) を開いた親ウィンドウへの参照を提供します。

### 基本的な動作
- `window.opener` は、新しいウィンドウやタブを `window.open()` で開いた場合に、その新しいウィンドウ内から元のウィンドウ (親ウィンドウ) を参照できます。
- 親ウィンドウが存在しない場合、`window.opener` は `null` になります。

### 使用例
#### 例 1: 新しいウィンドウを開き、親ウィンドウのデータを操作する
**親ウィンドウ (index.html):**
```html
<button onclick="openChild()">新しいウィンドウを開く</button>

<script>
function openChild() {
  window.open("child.html", "_blank", "width=400,height=300");
}
</script>
```

**子ウィンドウ (child.html):**
```html
<button onclick="sendMessage()">親ウィンドウにメッセージを送る</button>

<script>
function sendMessage() {
  if (window.opener) {
    window.opener.document.body.style.backgroundColor = 'lightblue';
    alert("親ウィンドウの背景色を変更しました");
  } else {
    alert("親ウィンドウが存在しません");
  }
}
</script>
```

### ポイント
- 子ウィンドウから親ウィンドウを操作できるため、クロスウィンドウの通信や操作が可能です。
- `window.opener` を使うことで、複数ウィンドウ間でデータをやり取りしたり、状態を同期することができます。

---

### セキュリティ面の注意
1. **オープナー攻撃 (Opener Exploit)**  
  - 悪意のあるサイトが `window.opener` を使って、親ウィンドウを操作・リダイレクトする可能性があります。  
  - これを防ぐために、新しいウィンドウを開く際に `rel="noopener noreferrer"` を指定します。
  
```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">新しいタブで開く</a>
```
- `noopener` があると、`window.opener` は `null` になります。
  
2. **クロスオリジン制約**  
  - 異なるオリジン (ドメイン) 間では、`window.opener` で DOM を操作できません。これはブラウザがクロスオリジンのセキュリティポリシー (CORS) によってブロックするためです。

---


`window.opener` で親画面から子画面を開く際に **Javaのコントローラーを経由させる** 
`window.open()` のURLとして **JavaのSpring BootやServletのエンドポイント** を指定し、そのエンドポイントで必要なデータを処理して子画面を表示する仕組みです。

### 方法の概要
1. 親ウィンドウで `window.open()` を使って子ウィンドウを開く。  
2. URLにJavaコントローラーのエンドポイントを指定する。  
3. Javaコントローラーで必要な処理を行い、子画面のHTMLやデータを返す。  
4. 子ウィンドウ内で `window.opener` を使って親ウィンドウと通信する。  

---

### 具体例 (Spring Boot を使用)
#### 1. 親ウィンドウから子ウィンドウを開く (JavaScript)
```html
<button onclick="openChild()">子ウィンドウを開く</button>

<script>
function openChild() {
  const url = '/child-page?param1=value1&param2=value2';
  window.open(url, '_blank', 'width=600,height=400');
}
</script>
```

---

#### 2. Javaコントローラー (Spring Boot)
```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class ChildWindowController {

    @GetMapping("/child-page")
    public String openChildPage(@RequestParam String param1, 
                                @RequestParam String param2, 
                                Model model) {
        // 必要な処理 (データ取得や加工)
        model.addAttribute("param1", param1);
        model.addAttribute("param2", param2);
        
        // 子ウィンドウのHTMLを返す
        return "child";  // resources/templates/child.html を返す
    }
}
```

---

#### 3. 子ウィンドウ (Thymeleaf などで表示)
**child.html (Thymeleaf)**
```html
<!DOCTYPE html>
<html>
<head>
    <title>子ウィンドウ</title>
</head>
<body>
    <h1>子ウィンドウの画面</h1>
    <p>パラメータ1: <span th:text="${param1}"></span></p>
    <p>パラメータ2: <span th:text="${param2}"></span></p>

    <button onclick="sendMessageToParent()">親ウィンドウにメッセージ送信</button>

    <script>
        function sendMessageToParent() {
            if (window.opener) {
                window.opener.document.body.style.backgroundColor = 'lightgreen';
                alert("親ウィンドウの背景色を変更しました");
            } else {
                alert("親ウィンドウが存在しません");
            }
        }
    </script>
</body>
</html>
```

---

### 説明
- **親ウィンドウから子ウィンドウを開くとき**に、`/child-page` というJavaコントローラーのエンドポイントを経由します。  
- パラメータ (`param1` や `param2`) をURLに付与して送信し、Java側で処理します。  
- Javaコントローラーがパラメータを受け取り、Thymeleafで子ウィンドウの画面を生成します。  
- 子ウィンドウから `window.opener` を使って親ウィンドウを操作することも可能です。

---

### 応用ポイント
- **データの動的取得**: Javaコントローラー内でデータベースや外部APIと連携して動的にデータを取得し、子ウィンドウに渡せます。  
- **状態管理**: セッションや`Model`を活用して、親ウィンドウから送られたデータを保持し、子ウィンドウで表示できます。  
- **非同期通信**: 子ウィンドウが開いた後も、`window.opener` を使って親ウィンドウと双方向で通信が可能です。  

---

### 注意点
1. **セキュリティ**:
   - 子ウィンドウから親ウィンドウを操作できるため、`rel="noopener"` を必要に応じて使用し、不正な操作を防ぎましょう。  
   
2. **クロスオリジン制約**:
   - 親ウィンドウと子ウィンドウが異なるオリジンの場合、`window.opener` は動作しません。  
   - 同一オリジンでの運用が推奨されます。  

3. **状態管理**:
   - 子ウィンドウが閉じられた際の処理など、親ウィンドウ側で子ウィンドウの状態を監視する仕組み (`setInterval` など) も実装可能です。

---

この方法を使えば、親ウィンドウと子ウィンドウでJavaコントローラーを介したデータ処理が柔軟に行えるようになります。
