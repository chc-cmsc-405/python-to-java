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

## Strings

### String Basics

| Concept | Python | Java |
|---------|--------|------|
| **Create** | `s = "hello"` | `String s = "hello";` |
| **Length** | `len(s)` | `s.length()` |
| **Concatenate** | `s1 + s2` | `s1 + s2` |
| **Access char** | `s[0]` | `s.charAt(0)` |
| **Check empty** | `if not s:` | `if (s.isEmpty())` |
| **Uppercase** | `s.upper()` | `s.toUpperCase()` |
| **Lowercase** | `s.lower()` | `s.toLowerCase()` |
| **Strip whitespace** | `s.strip()` | `s.trim()` |
| **Split** | `s.split(",")` | `s.split(",")` |

### String Operations (Finding & Extracting)

| Concept | Python | Java |
|---------|--------|------|
| **Find** | `s.find("ell")` | `s.indexOf("ell")` |
| **Find from end** | `s.rfind("l")` | `s.lastIndexOf("l")` |
| **Substring** | `s[1:4]` | `s.substring(1, 4)` (start, end) |
| **Contains** | `"ell" in s` | `s.contains("ell")` |
| **Starts with** | `s.startswith("He")` | `s.startsWith("He")` |
| **Ends with** | `s.endswith("!")` | `s.endsWith("!")` |

```java
String text = "Hello, World!";
System.out.println(text.indexOf("o"));        // 4
System.out.println(text.lastIndexOf("o"));    // 8
System.out.println(text.substring(0, 5));     // Hello
System.out.println(text.startsWith("Hello")); // true
```

### String Modifiers

Java strings are **immutable**—methods return new strings, they don't modify the original.

| Concept | Python | Java |
|---------|--------|------|
| **Replace all** | `s.replace("o", "0")` | `s.replace("o", "0")` |
| **Replace first** | N/A | `s.replaceFirst("o", "0")` |
| **Join** | `",".join(list)` | `String.join(",", list)` |

```java
String text = "Hello, World!";
System.out.println(text.replace("o", "0"));      // Hell0, W0rld!
System.out.println(text.replaceFirst("o", "0")); // Hell0, World!
// Original 'text' is unchanged
```

### String Comparison

**Important:** Always use `.equals()` for String comparison:

```java
String s1 = "hello";
String s2 = "hello";

// WRONG (compares references)
if (s1 == s2) { }

// CORRECT (compares content)
if (s1.equals(s2)) { }

// Case-insensitive comparison
if (s1.equalsIgnoreCase("HELLO")) { }
```

## Character Functions

Java provides character functions in the `Character` class. In Python, these are methods on strings. In Java, they're static methods that take a character.

| Task | Python | Java |
|------|--------|------|
| **Is letter?** | `c.isalpha()` | `Character.isLetter(c)` |
| **Is digit?** | `c.isdigit()` | `Character.isDigit(c)` |
| **Is alphanumeric?** | `c.isalnum()` | `Character.isLetterOrDigit(c)` |
| **Is whitespace?** | `c.isspace()` | `Character.isWhitespace(c)` |
| **Is uppercase?** | `c.isupper()` | `Character.isUpperCase(c)` |
| **Is lowercase?** | `c.islower()` | `Character.isLowerCase(c)` |
| **To uppercase** | `c.upper()` | `Character.toUpperCase(c)` |
| **To lowercase** | `c.lower()` | `Character.toLowerCase(c)` |

**Python:**
```python
text = "Hello123"
for c in text:
    if c.isalpha():
        print(c.upper())
    elif c.isdigit():
        print(c)
```

**Java:**
```java
String text = "Hello123";
for (char c : text.toCharArray()) {
    if (Character.isLetter(c)) {
        System.out.print(Character.toUpperCase(c));
    } else if (Character.isDigit(c)) {
        System.out.print(c);
    }
}
```

---

[← Previous: Functions](05-functions.md) | [Next: I/O Streams →](07-io-streams.md)
