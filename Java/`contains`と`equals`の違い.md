Javaの`contains`と`equals`の違いについて解説します。

### **1. `contains` メソッド**
`contains`は、コレクション（例: `List`, `Set`）や文字列（`String`）などのクラスで使用されるメソッドで、対象の要素や部分文字列が含まれているかどうかを判定します。

#### **① `String#contains()`**
`String` クラスの `contains()` メソッドは、指定した部分文字列が含まれているかどうかを確認します。

```java
public class ContainsExample {
    public static void main(String[] args) {
        String str = "Hello, Java!";
        System.out.println(str.contains("Java"));  // true
        System.out.println(str.contains("World")); // false
    }
}
```

**特徴:**
- 引数には`CharSequence`（`String`など）を取る
- 大文字・小文字を区別する
- 部分文字列の一致をチェックする

#### **② `Collection#contains()`**
`List`や`Set`などのコレクションが、指定した要素を含んでいるかをチェックします。

```java
import java.util.*;

public class CollectionContainsExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        System.out.println(list.contains("Banana")); // true
        System.out.println(list.contains("Grape"));  // false
    }
}
```

**特徴:**
- `contains`メソッドは、`equals`メソッドを使って比較を行う
- `Set`や`List`で利用可能
- `HashSet`では`hashCode()`と`equals()`を使用して検索されるため、高速な検索が可能

---

### **2. `equals` メソッド**
`equals`は、オブジェクト同士が「意味的に等しいか」を判定するためのメソッドです。

#### **① `String#equals()`**
`String`クラスでの`equals()`メソッドは、2つの文字列が完全に一致するかを比較します。

```java
public class EqualsExample {
    public static void main(String[] args) {
        String str1 = "Java";
        String str2 = "Java";
        String str3 = new String("Java");

        System.out.println(str1.equals(str2)); // true
        System.out.println(str1.equals(str3)); // true
        System.out.println(str1 == str3);      // false (異なるオブジェクト参照)
    }
}
```

**特徴:**
- 完全一致をチェックする
- `equalsIgnoreCase()`を使えば大文字小文字を無視できる

#### **② `Object#equals()`**
クラスのオブジェクトを比較する場合、`equals()`メソッドをオーバーライドしないと、デフォルトの`equals()`（`Object`クラスの実装）は「参照アドレスが同じかどうか」しか比較しません。

```java
class Person {
    String name;

    Person(String name) {
        this.name = name;
    }
}

public class EqualsObjectExample {
    public static void main(String[] args) {
        Person p1 = new Person("Alice");
        Person p2 = new Person("Alice");

        System.out.println(p1.equals(p2)); // false（デフォルトのequalsは参照比較）
    }
}
```

`equals()`をオーバーライドすれば、意味的な等価性を比較できます。

```java
class Person {
    String name;

    Person(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return name.equals(person.name);
    }
}

public class EqualsOverrideExample {
    public static void main(String[] args) {
        Person p1 = new Person("Alice");
        Person p2 = new Person("Alice");

        System.out.println(p1.equals(p2)); // true
    }
}
```

---

### **3. `contains` と `equals` の違い**
|  | `contains()` | `equals()` |
|---|---|---|
| **主な用途** | 部分文字列や要素の存在チェック | オブジェクトの等価性チェック |
| **データ型** | `String`, `List`, `Set` など | すべてのオブジェクト |
| **比較方法** | `equals()`を内部で使用して判定 | `equals()`を直接使用して判定 |
| **部分一致** | 可能（`String`の場合） | できない（完全一致のみ） |
| **オーバーライドの必要性** | なし（`String`や`List`の内部実装を利用） | `Object`のデフォルトでは参照比較なので、オーバーライド推奨 |

---

### **4. まとめ**
- **`contains()`** は「部分一致」を調べるメソッドで、リストや文字列に含まれているかをチェックする。
- **`equals()`** は「完全一致」を調べるメソッドで、2つのオブジェクトが意味的に等しいかを比較する。
- **`contains()`の内部では`equals()`が使われる**（例えば`List.contains()`は各要素と`equals()`で比較する）。
- **カスタムクラスを使う場合、`equals()`をオーバーライドしないと意図しない動作になる可能性がある**。
