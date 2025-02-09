`Map<String, Object>` 型のデータを DTO クラスに詰め込むには、以下のような方法が考えられます。

## 方法1: Jackson の `ObjectMapper` を使う
Jackson の `ObjectMapper` を使うと、`Map<String, Object>` から DTO クラスへの変換を簡単に行えます。

### 実装手順
1. `ObjectMapper` を使用して `Map<String, Object>` を JSON に変換する。
2. JSON から DTO クラスに変換する。

### サンプルコード
```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.util.Map;

public class Main {
    public static void main(String[] args) throws Exception {
        // サンプルの Map データ
        Map<String, Object> data = Map.of(
            "id", 1,
            "name", "John Doe",
            "age", 30
        );

        // ObjectMapper を使って DTO に変換
        ObjectMapper objectMapper = new ObjectMapper();
        UserDto userDto = objectMapper.convertValue(data, UserDto.class);

        // 結果を表示
        System.out.println(userDto);
    }
}

// DTO クラス
class UserDto {
    private int id;
    private String name;
    private int age;

    // ゲッターとセッター
    public int getId() { return id; }
    public void setId(int id) { this.id = id; }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }

    @Override
    public String toString() {
        return "UserDto{id=" + id + ", name='" + name + "', age=" + age + "}";
    }
}
```

### 実行結果
```
UserDto{id=1, name='John Doe', age=30}
```

---

## 方法2: 手動で詰め替える
Jackson なしで手動で `Map` から DTO に詰め替える場合、以下のように `Map#get` を使って値を取得し、適切な型にキャストして DTO にセットします。

### サンプルコード
```java
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        // サンプルの Map データ
        Map<String, Object> data = Map.of(
            "id", 1,
            "name", "John Doe",
            "age", 30
        );

        // 手動で DTO に詰め替え
        UserDto userDto = new UserDto();
        userDto.setId((Integer) data.get("id"));
        userDto.setName((String) data.get("name"));
        userDto.setAge((Integer) data.get("age"));

        // 結果を表示
        System.out.println(userDto);
    }
}
```

### メリット・デメリット
| 方法 | メリット | デメリット |
|------|--------|----------|
| Jackson `ObjectMapper` | コードが簡潔で、メンテナンスしやすい | 依存ライブラリが必要 |
| 手動詰め替え | 依存ライブラリ不要、細かい制御が可能 | フィールド数が多い場合、コードが冗長になる |

---

**おすすめ:**  
- **Jackson の `ObjectMapper` を使う** ほうが、可読性・メンテナンス性が高くなるので、特に Spring Boot や REST API で扱う場合は `ObjectMapper` の使用を推奨します。
- もし **パフォーマンスを重視** する場合や **外部ライブラリを使いたくない** 場合は、手動で詰め替える方法もありです。

