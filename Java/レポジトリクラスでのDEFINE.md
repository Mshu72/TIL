**`DEFINE` は Java のレポジトリクラス（たとえば JDBC、MyBatis、JPA など）では使用できません。**

---

###  `DEFINE` は SQL*Plus や SQL Developer 専用

- `DEFINE` は Oracle の **SQL*Plus や SQL Developer など、対話型SQLツールのスクリプト用**です。
- Javaなどのアプリケーションコードから実行するSQLには使えません。

---

###  Javaから定数のように値を渡す方法

Javaのレポジトリクラスでは、**プレースホルダ付きSQL + パラメータバインド**を使うのが一般的です。

####  JDBCの例：

```java
String sql = "SELECT ENV_VAL1, ENV_VAL2 " +
             "FROM BR_MST_ENV " +
             "WHERE ENV_KEY1 = ? AND ENV_KEY2 = ? AND ENV_KEY3 = ? AND ENV_SEQ = ?";

PreparedStatement stmt = connection.prepareStatement(sql);
stmt.setString(1, "四日市");
stmt.setString(2, "*");
stmt.setString(3, "*");
stmt.setInt(4, 1);

ResultSet rs = stmt.executeQuery();
```

####  MyBatisの例：

```xml
<select id="selectEnv" resultType="Env">
  SELECT ENV_VAL1, ENV_VAL2
  FROM BR_MST_ENV
  WHERE ENV_KEY1 = #{envKey1}
    AND ENV_KEY2 = #{envKey2}
    AND ENV_KEY3 = #{envKey3}
    AND ENV_SEQ  = #{envSeq}
</select>
```

```java
// 呼び出し側
Map<String, Object> params = new HashMap<>();
params.put("envKey1", "四日市");
params.put("envKey2", "*");
params.put("envKey3", "*");
params.put("envSeq", 1);

List<Env> result = envMapper.selectEnv(params);
```

---

###  補足：もし「SQL内に定数っぽく値を定義したい」なら？

Java側でSQLを組み立てるとき、変数のように **final 定数** を使うことは可能です：

```java
final String ENV_KEY1 = "四日市";
final String ENV_KEY2 = "*";
final String ENV_KEY3 = "*";
final int ENV_SEQ = 1;
```

こうすれば、ソースコード内の「定数」としてSQLを管理できます。

