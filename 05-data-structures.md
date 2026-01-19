# 05 - Data Structures

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

| Concept | Python | Java |
|---------|--------|------|
| **Create** | `s = "hello"` | `String s = "hello";` |
| **Length** | `len(s)` | `s.length()` |
| **Concatenate** | `s1 + s2` | `s1 + s2` |
| **Find** | `s.find("ell")` | `s.indexOf("ell")` |
| **Substring** | `s[1:4]` | `s.substring(1, 4)` (start, end) |
| **Access char** | `s[0]` | `s.charAt(0)` |
| **Uppercase** | `s.upper()` | `s.toUpperCase()` |
| **Lowercase** | `s.lower()` | `s.toLowerCase()` |
| **Strip whitespace** | `s.strip()` | `s.trim()` |
| **Split** | `s.split(",")` | `s.split(",")` |
| **Contains** | `"ell" in s` | `s.contains("ell")` |

**Python:**
```python
text = "Hello, World!"
print(len(text))          # 13
print(text[0:5])          # Hello
print(text.find("World")) # 7
print(text.upper())       # HELLO, WORLD!
```

**Java:**
```java
String text = "Hello, World!";
System.out.println(text.length());           // 13
System.out.println(text.substring(0, 5));    // Hello
System.out.println(text.indexOf("World"));   // 7
System.out.println(text.toUpperCase());      // HELLO, WORLD!
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

---

## File I/O

Java provides several ways to read and write files. The most common approaches use `BufferedReader` for reading and `PrintWriter` for writing. Java 7+ introduced try-with-resources for automatic cleanup.

### Reading a File

**Python:**
```python
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

**Java:**
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

try (BufferedReader reader = new BufferedReader(new FileReader("data.txt"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    System.out.println("Error reading file: " + e.getMessage());
}
```

### Writing to a File

**Python:**
```python
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
```

**Java:**
```java
import java.io.PrintWriter;
import java.io.IOException;

try (PrintWriter writer = new PrintWriter("output.txt")) {
    writer.println("Hello, World!");
} catch (IOException e) {
    System.out.println("Error writing file: " + e.getMessage());
}
```

### Common File Operations

| Task | Python | Java |
|------|--------|------|
| **Open for reading** | `open("f.txt", "r")` | `new BufferedReader(new FileReader("f.txt"))` |
| **Open for writing** | `open("f.txt", "w")` | `new PrintWriter("f.txt")` |
| **Read line** | `line = file.readline()` | `line = reader.readLine()` |
| **Read all lines** | `for line in file:` | `while ((line = reader.readLine()) != null)` |
| **Write line** | `file.write(text + "\n")` | `writer.println(text)` |
| **Auto-close** | `with open(...) as f:` | `try (Reader r = ...) { }` |

### Reading CSV Data

**Python:**
```python
with open("data.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name = parts[0]
        score = int(parts[1])
```

**Java:**
```java
import java.io.BufferedReader;
import java.io.FileReader;

try (BufferedReader reader = new BufferedReader(new FileReader("data.csv"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        String[] parts = line.split(",");
        String name = parts[0];
        int score = Integer.parseInt(parts[1]);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### Using Scanner (Alternative)

`Scanner` is simpler for basic input but less efficient for large files:

```java
import java.io.File;
import java.util.Scanner;

try (Scanner scanner = new Scanner(new File("data.txt"))) {
    while (scanner.hasNextLine()) {
        String line = scanner.nextLine();
        System.out.println(line);
    }
} catch (Exception e) {
    e.printStackTrace();
}
```

### Try-With-Resources

Java 7+ automatically closes resources declared in the try statement:

```java
// Resources are automatically closed when the block exits
try (
    BufferedReader reader = new BufferedReader(new FileReader("input.txt"));
    PrintWriter writer = new PrintWriter("output.txt")
) {
    String line;
    while ((line = reader.readLine()) != null) {
        writer.println(line.toUpperCase());
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

---

[← Previous: Control Flow](04-control-flow.md) | [Next: Functions →](06-functions.md)
