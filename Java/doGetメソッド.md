`doGet` は、Javaのサーブレットで使用されるメソッドの1つで、HTTP GETリクエストに対応するために使われます。サーブレットはJava EE（Enterprise Edition）環境で動作し、クライアント（通常はWebブラウザ）からのリクエストを処理するWebアプリケーションのコンポーネントです。

### `doGet` メソッドの特徴と使い方
- **役割**: クライアントからGETリクエストを受け取ったときに呼び出されるメソッドです。GETリクエストは、通常ブラウザがサーバーに対してページやデータを要求する際に使用されます。例えば、ユーザーがURLを入力してWebページにアクセスすると、ブラウザはGETリクエストをサーバーに送信します。
- **メソッドのシグネチャ**: サーブレットでGETリクエストを処理するために、`HttpServlet` クラスを継承し、`doGet` メソッドをオーバーライドします。

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {
    // リクエスト処理の実装
}
```

- **パラメータ**:
  - `HttpServletRequest request`: クライアントから送られてきたリクエスト情報を表します。これには、パラメータ、ヘッダー、クエリ文字列などが含まれます。
  - `HttpServletResponse response`: サーバーからクライアントに送信するレスポンスを表します。このオブジェクトを使用して、HTMLページやデータを返すことができます。

### `doGet` の流れ
1. クライアントがGETリクエストを送信します（例えば、URLのクエリパラメータを含むリクエスト）。
2. サーブレットコンテナがクライアントのリクエストを受け取り、適切なサーブレットを呼び出します。
3. サーブレットは`doGet` メソッドを実行し、リクエストを処理します。
4. `HttpServletResponse` オブジェクトを使って、サーバーはHTML、JSON、XMLなどのデータをクライアントに返します。

### 例: 簡単な`doGet` メソッド

```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // コンテンツタイプを設定 (例: HTMLページ)
        response.setContentType("text/html");

        // レスポンスの出力ストリームを取得
        PrintWriter out = response.getWriter();
        
        // HTMLの出力
        out.println("<html><body>");
        out.println("<h1>Hello, Servlet World!</h1>");
        out.println("</body></html>");
    }
}
```

### 実行例
ブラウザから`http://localhost:8080/HelloServlet`のようにリクエストを送ると、このサーブレットが呼び出され、ブラウザに「Hello, Servlet World!」というメッセージを表示するHTMLページが返されます。

### まとめ
- `doGet`はGETリクエストに対応するためのサーブレットメソッドです。
- 主にデータを要求したりページを表示するためのリクエスト処理に使用されます。
- `HttpServletRequest` でクライアントからのリクエスト情報を取得し、`HttpServletResponse` でその結果をクライアントに返す仕組みです。
