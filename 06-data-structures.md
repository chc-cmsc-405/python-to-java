# 06 - Data Structures

[← Back to Java Guide](README.md)

Java provides data structures through its Collections Framework. `ArrayList` is most similar to Python's list—a resizable array that grows automatically. Unlike Python lists, Java collections can only hold objects (not primitives), so you use wrapper classes (`Integer` instead of `int`). `HashMap` works like Python dictionaries but also requires type declarations for both keys and values.

---

## Arrays vs ArrayLists

Java has two options: **fixed-size arrays** and **resizable ArrayLists**.

### Fixed Arrays

| Concept | Python | Java |
|---------|--------|------|
| **Create** | `[1, 2, 3]` | `int[] arr = {1, 2, 3};` |
| **Create empty** | `[None] * 5` | `int[] arr = new int[5];` |
| **Access** | `arr[0]` | `arr[0]` |
| **Length** | `len(arr)` | `arr.length` |

**Java arrays cannot be resized after creation:**
```java
int[] numbers = new int[3];    // Fixed size of 3
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
// numbers[3] = 40;  // Error! Array index out of bounds
```

### ArrayList (Resizable)

| Concept | Python | Java |
|---------|--------|------|
| **Create** | `my_list = []` | `ArrayList<Integer> list = new ArrayList<>();` |
| **Create with items** | `[1, 2, 3]` | `new ArrayList<>(Arrays.asList(1, 2, 3))` |
| **Access** | `list[0]` | `list.get(0)` |
| **Set** | `list[0] = 5` | `list.set(0, 5)` |
| **Length** | `len(list)` | `list.size()` |
| **Append** | `list.append(4)` | `list.add(4);` |
| **Insert** | `list.insert(1, x)` | `list.add(1, x);` |
| **Remove** | `list.remove(x)` | `list.remove(Integer.valueOf(x));` |
| **Remove by index** | `list.pop(1)` | `list.remove(1);` |
| **Check empty** | `if not list:` | `if (list.isEmpty())` |
| **Contains** | `x in list` | `list.contains(x)` |

**Python:**
```python
numbers = [1, 2, 3, 4, 5]
numbers.append(6)
print(numbers[0])     # 1
print(len(numbers))   # 6
```

**Java:**
```java
import java.util.ArrayList;

ArrayList<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.add(3);
numbers.add(6);
System.out.println(numbers.get(0));    // 1
System.out.println(numbers.size());    // 4
```

## Iterating Over Collections

**Python:**
```python
for num in numbers:
    print(num)

for i, num in enumerate(numbers):
    print(f"{i}: {num}")
```

**Java:**
```java
// Enhanced for loop
for (int num : numbers) {
    System.out.println(num);
}

// With index
for (int i = 0; i < numbers.size(); i++) {
    System.out.println(i + ": " + numbers.get(i));
}
```

## Dictionaries / HashMaps

| Concept | Python | Java |
|---------|--------|------|
| **Create** | `d = {}` | `HashMap<String, Integer> map = new HashMap<>();` |
| **Create with items** | `{"a": 1, "b": 2}` | Use `map.put()` for each item |
| **Access** | `d["a"]` | `map.get("a")` |
| **Check key** | `"a" in d` | `map.containsKey("a")` |
| **Add/Update** | `d["c"] = 3` | `map.put("c", 3);` |
| **Delete** | `del d["a"]` | `map.remove("a");` |
| **Get keys** | `d.keys()` | `map.keySet()` |
| **Get values** | `d.values()` | `map.values()` |

**Python:**
```python
scores = {"Alice": 95, "Bob": 87}
scores["Charlie"] = 92

if "Alice" in scores:
    print(scores["Alice"])

for name, score in scores.items():
    print(f"{name}: {score}")
```

**Java:**
```java
import java.util.HashMap;

HashMap<String, Integer> scores = new HashMap<>();
scores.put("Alice", 95);
scores.put("Bob", 87);
scores.put("Charlie", 92);

if (scores.containsKey("Alice")) {
    System.out.println(scores.get("Alice"));
}

for (String name : scores.keySet()) {
    System.out.println(name + ": " + scores.get(name));
}
```

---

[← Previous: Functions](05-functions.md) | [Next: I/O Streams →](07-io-streams.md)
