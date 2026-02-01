# 07 - I/O Streams

[← Back to Java Guide](README.md)

Java provides several ways to read and write files. The most common approaches use `BufferedReader` for reading and `PrintWriter` for writing. Java 7+ introduced try-with-resources for automatic cleanup. This section covers file I/O—for console I/O (`Scanner` with `System.in`), see [01-basics](01-basics.md).

---

## Reading a File

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

## Writing to a File

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

## Common File Operations

| Task | Python | Java |
|------|--------|------|
| **Open for reading** | `open("f.txt", "r")` | `new BufferedReader(new FileReader("f.txt"))` |
| **Open for writing** | `open("f.txt", "w")` | `new PrintWriter("f.txt")` |
| **Read line** | `line = file.readline()` | `line = reader.readLine()` |
| **Read all lines** | `for line in file:` | `while ((line = reader.readLine()) != null)` |
| **Write line** | `file.write(text + "\n")` | `writer.println(text)` |
| **Auto-close** | `with open(...) as f:` | `try (Reader r = ...) { }` |

## Reading CSV Data

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

## Using Scanner for Files

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

## Try-With-Resources

Java 7+ automatically closes resources declared in the try statement—similar to Python's `with` statement:

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

## Common I/O Classes

| Class | Purpose |
|-------|---------|
| `FileReader` | Read characters from a file |
| `BufferedReader` | Efficient line-by-line reading |
| `FileWriter` | Write characters to a file |
| `PrintWriter` | Convenient formatted output |
| `Scanner` | Simple parsing of text input |

## Required Imports

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.PrintWriter;
import java.io.IOException;
import java.io.File;
import java.util.Scanner;
```

---

[← Previous: Data Structures](06-data-structures.md) | [Next: Custom Types →](08-custom-types.md)
