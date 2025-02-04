Javaの`Stream` APIにある`noneMatch`メソッドは、ストリーム内の要素がすべて条件を満たさない場合に`true`を返すメソッドです。

## **`noneMatch` メソッドの概要**
```java
boolean noneMatch(Predicate<? super T> predicate)
```
- **引数**: `Predicate<T>` (ラムダ式やメソッド参照を使って、条件を指定)
- **戻り値**: `boolean`
  - 条件を満たす要素が **1つもない** 場合は `true`
  - 条件を満たす要素が **1つでもある** 場合は `false`
- **短絡評価 (Short-circuiting)**:
  - 条件を満たす要素が見つかった時点で `false` を返し、それ以降の処理をスキップする。

---

## **使用例**
### **1. 全ての要素が条件を満たさない場合**
```java
import java.util.Arrays;
import java.util.List;

public class NoneMatchExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // すべての要素が10以上でないかチェック
        boolean result = numbers.stream().noneMatch(n -> n >= 10);

        System.out.println(result);  // true (全て10未満)
    }
}
```
**解説**:
- `numbers` の中に `10以上` の数が **1つもない** ため、`noneMatch` は `true` を返す。

---

### **2. 条件を満たす要素がある場合**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// すべての要素が3未満でないかチェック
boolean result = numbers.stream().noneMatch(n -> n < 3);

System.out.println(result);  // false (1, 2が条件を満たす)
```
**解説**:
- `numbers` の中に `3未満` の数 (`1` や `2`) があるため、`noneMatch` は `false` を返す。

---

### **3. 空のストリームに対する動作**
```java
List<Integer> emptyList = Arrays.asList();

// 空のリストでnoneMatchを使用
boolean result = emptyList.stream().noneMatch(n -> n > 0);

System.out.println(result);  // true (要素がないので条件を満たすものもない)
```
**解説**:
- 空のストリームでは、条件を満たす要素が存在しないため `true` を返す。

---

## **`anyMatch`・`allMatch` との比較**
| メソッド        | 条件を満たす要素が1つでもあれば `true` | すべての要素が条件を満たせば `true` | 1つも条件を満たさなければ `true` |
|---------------|--------------------------|--------------------------|--------------------------|
| `anyMatch`    | ✅ (1つでも該当すれば `true`) | ❌ | ❌ |
| `allMatch`    | ❌ | ✅ (全て該当すれば `true`) | ❌ |
| `noneMatch`   | ❌ | ❌ | ✅ (1つも該当しなければ `true`) |

---

## **まとめ**
- `noneMatch` は **すべての要素が条件を満たさない** 場合に `true` を返す。
- **短絡評価** のため、条件を満たす要素が見つかると即座に `false` を返す。
- 空のストリームに対しては、`true` を返す。

使いどころとしては、リスト内に特定の値が **含まれていないことを確認する** 場面などで有効です。
