`JsonNode` は、Jacksonライブラリで提供されるクラスで、JSONデータをオブジェクトツリーの形式で表現するために使用されます。`JsonNode` は Jackson の `ObjectMapper` クラスを使って JSON 文字列を解析することで生成され、JSONデータをノード（ツリー構造）として操作できます。

### Jacksonの概要
JacksonはJavaで人気のあるJSON処理ライブラリで、JSONデータの解析（パース）、生成、変換を効率的に行うことができます。`JsonNode`は、その中でも「ツリー型モデル」と呼ばれる方法でJSONデータを扱うための中心的なクラスです。

---

## JsonNodeの特徴
- **Immutable（不変）**  
  `JsonNode` は基本的に不変です。ノードの値を直接変更することはできませんが、新しいノードを作成して置き換えることができます。

- **ツリー構造**  
  JSONオブジェクトや配列が階層的に表現され、ルートノードから子ノードにアクセスすることで、ツリーをたどることができます。

- **柔軟な型サポート**  
  `ObjectNode`（オブジェクト型）、`ArrayNode`（配列型）、`TextNode`（文字列型）、`IntNode`（整数型）などの具象クラスがあり、`JsonNode`はこれらの親クラスです。

---

## 使用例

### 1. 基本的なJSONパース
```java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;

public class JsonNodeExample {
    public static void main(String[] args) throws Exception {
        String jsonString = "{ \"name\": \"Alice\", \"age\": 30, \"city\": \"Tokyo\" }";
        
        ObjectMapper mapper = new ObjectMapper();
        JsonNode rootNode = mapper.readTree(jsonString);
        
        String name = rootNode.get("name").asText();
        int age = rootNode.get("age").asInt();
        String city = rootNode.get("city").asText();
        
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("City: " + city);
    }
}
```

#### 解説
- `ObjectMapper` を使って、JSON文字列を `JsonNode` に変換しています。  
- `.get("name")` でJSONオブジェクトのフィールドにアクセスし、`asText()` で文字列として取得します。  
- 型に応じて `asInt()`, `asBoolean()`, `asDouble()` などのメソッドが利用できます。

---

### 2. JsonNodeの作成と変更
```java
import com.fasterxml.jackson.databind.node.ObjectNode;
import com.fasterxml.jackson.databind.ObjectMapper;

public class CreateJsonNode {
    public static void main(String[] args) throws Exception {
        ObjectMapper mapper = new ObjectMapper();
        ObjectNode rootNode = mapper.createObjectNode();
        
        rootNode.put("name", "Bob");
        rootNode.put("age", 25);
        rootNode.put("city", "Osaka");
        
        String jsonString = mapper.writerWithDefaultPrettyPrinter().writeValueAsString(rootNode);
        System.out.println(jsonString);
    }
}
```

#### 解説
- `ObjectNode` を直接生成し、`put` メソッドで値を追加しています。
- `writeValueAsString` でJSON文字列に変換して出力します。

---

## JsonNodeの主要メソッド
- **`get(String fieldName)`** : 指定したフィールドの値を取得  
- **`path(String fieldName)`** : フィールドが存在しない場合でも空のノードを返す（`null`を避けられる）  
- **`asText()`** : ノードを文字列として取得  
- **`asInt()`** : ノードを整数として取得  
- **`isObject()`** : オブジェクトかどうかを判定  
- **`isArray()`** : 配列かどうかを判定  
- **`size()`** : 配列やオブジェクトの要素数を取得  

---

## JsonNodeの用途
- **APIレスポンスの解析**  
  REST APIからのJSONレスポンスを解析して、必要なデータを抽出できます。  
- **JSONバリデーション**  
  JSONの構造が期待通りかどうかをチェックするのに便利です。  
- **設定ファイルの処理**  
  JSON形式の設定ファイルを解析して動的に処理できます。

Jacksonの `JsonNode` は非常に柔軟で便利なクラスです。JSONデータを扱う機会が多いJavaアプリケーションでは、習得しておくと非常に役立ちます。
