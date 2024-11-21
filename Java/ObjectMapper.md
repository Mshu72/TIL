`ObjectMapper` は、Javaで広く使用されるライブラリ [Jackson](https://github.com/FasterXML/jackson) の一部で、JSONとJavaオブジェクト間の変換を簡単に行える強力なツールです。以下で詳しく解説します。

---

## 主な用途
1. **JavaオブジェクトをJSON文字列に変換（シリアライズ）**
   - JavaのオブジェクトをJSON形式に変換します。
   
2. **JSON文字列をJavaオブジェクトに変換（デシリアライズ）**
   - JSON形式の文字列をJavaのオブジェクトに変換します。

3. **JSONデータの読み取り・書き出し**
   - ファイルやストリームから直接JSONを処理できます。

---

## 基本的な使い方

### 1. `ObjectMapper`のインスタンス化
```java
ObjectMapper mapper = new ObjectMapper();
```

### 2. シリアライズ（Javaオブジェクト → JSON文字列）
```java
public class Person {
    private String name;
    private int age;

    // GetterとSetterが必要
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
}

Person person = new Person();
person.setName("John");
person.setAge(30);

ObjectMapper mapper = new ObjectMapper();
String jsonString = mapper.writeValueAsString(person);
System.out.println(jsonString);  // {"name":"John","age":30}
```

### 3. デシリアライズ（JSON文字列 → Javaオブジェクト）
```java
String json = "{\"name\":\"John\",\"age\":30}";

Person person = mapper.readValue(json, Person.class);
System.out.println(person.getName());  // John
System.out.println(person.getAge());   // 30
```

---

## 特徴・カスタマイズ

### 1. **フィールド名のカスタマイズ**
- デフォルトでは、フィールド名はそのまま使用されますが、アノテーションを使用してカスタマイズできます。

#### フィールド名を変更する例
```java
import com.fasterxml.jackson.annotation.JsonProperty;

public class Person {
    @JsonProperty("full_name")
    private String name;

    @JsonProperty("age_years")
    private int age;

    // GetterとSetter
}
```

生成されるJSON:
```json
{"full_name":"John","age_years":30}
```

---

### 2. **非標準のデータ形式の処理**
- 特定のフォーマット（例：カスタム日付フォーマット）を処理できます。

#### カスタム日付フォーマット
```java
import com.fasterxml.jackson.annotation.JsonFormat;
import java.util.Date;

public class Event {
    private String name;

    @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd")
    private Date date;

    // GetterとSetter
}
```

---

### 3. **カスタムシリアライザー/デシリアライザー**
- 独自の変換ロジックを定義することができます。

#### シリアライザーの例
```java
import com.fasterxml.jackson.core.JsonGenerator;
import com.fasterxml.jackson.databind.JsonSerializer;
import com.fasterxml.jackson.databind.SerializerProvider;

import java.io.IOException;

public class CustomSerializer extends JsonSerializer<String> {
    @Override
    public void serialize(String value, JsonGenerator gen, SerializerProvider serializers) throws IOException {
        gen.writeString(value.toUpperCase());  // 大文字に変換して出力
    }
}
```

適用方法:
```java
import com.fasterxml.jackson.databind.annotation.JsonSerialize;

public class Person {
    @JsonSerialize(using = CustomSerializer.class)
    private String name;

    // GetterとSetter
}
```

---

## メリット
1. **シンプルで強力**:
   - 少ないコードでJSONとJavaオブジェクトの相互変換が可能。
   
2. **高い拡張性**:
   - アノテーションやカスタムシリアライザーなどで柔軟にカスタマイズ可能。

3. **広範な機能**:
   - JSON以外のフォーマット（YAMLやXML）も処理可能（モジュールを追加）。

---

## 注意点
1. **Getter/Setterが必要**
   - デフォルトでは、JacksonはJava Beans形式（Getter/Setter）を前提に動作します。
   
2. **デフォルトの挙動に注意**
   - 未知のプロパティを含むJSONを処理する場合、エラーになることがあります。この場合、以下の設定で緩和可能です。
     ```java
     mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
     ```

3. **パフォーマンス**
   - `ObjectMapper`のインスタンスは重いので、必要に応じて再利用するのがベストプラクティスです。

---

Jacksonの`ObjectMapper`は、JSONの処理を効率化するための非常に強力なツールで、多くのJavaプロジェクトで標準的に採用されています。
