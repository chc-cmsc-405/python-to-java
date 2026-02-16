# 09 - Java Unique Features

[← Back to Java Guide](README.md)

These concepts don't have direct Python equivalents or work significantly differently. Java's exception handling is more structured than Python's, with checked exceptions requiring explicit handling. Java and Python both use garbage collection, but their approaches differ.

## Contents

- [Memory Management: Python vs Java](#memory-management-python-vs-java)
- [Exception Handling](#exception-handling)

---

## Memory Management: Python vs Java

Both Python and Java use garbage collection, but with important differences:

| Aspect | Python | Java |
|--------|--------|------|
| **Memory management** | Automatic (GC) | Automatic (GC) |
| **Garbage collector** | Reference counting + cycle detection | Generational GC (tunable) |
| **Manual deallocation** | Not possible | Not possible |
| **Memory leaks** | Rare (circular references) | Rare (holding references) |
| **GC control** | Limited | Extensive (JVM flags) |

**Python GC:**
```python
def process_data():
    data = [1, 2, 3, 4, 5]  # Allocated
    return sum(data)
    # 'data' cleaned up automatically when reference count hits 0
```

**Java GC:**
```java
public void processData() {
    ArrayList<Integer> data = new ArrayList<>();  // Allocated on heap
    data.add(1);
    data.add(2);
    // When method ends and 'data' goes out of scope,
    // it becomes eligible for garbage collection
}
```

**Key difference:** You never explicitly free memory in Java (no `delete` like C++), but you should:
- Set large objects to `null` when done
- Close resources (files, connections) properly
- Avoid holding references longer than needed

## Exception Handling

Java has **checked exceptions** that must be handled or declared. Python has no equivalent concept.

### Basic Try-Catch

**Python:**
```python
try:
    result = risky_operation()
except ValueError as e:
    print(f"Error: {e}")
finally:
    cleanup()
```

**Java:**
```java
try {
    int result = riskyOperation();
} catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    cleanup();
}
```

### Checked vs Unchecked Exceptions

Java distinguishes between:
- **Checked exceptions:** Must be caught or declared with `throws`
- **Unchecked exceptions:** Optional to handle (RuntimeException and subclasses)

```java
// Checked exception - MUST handle or declare
public void readFile(String path) throws IOException {
    FileReader reader = new FileReader(path);  // May throw IOException
}

// Or catch it
public void readFile(String path) {
    try {
        FileReader reader = new FileReader(path);
    } catch (IOException e) {
        System.out.println("Could not read file");
    }
}

// Unchecked exception - optional to handle
public int divide(int a, int b) {
    return a / b;  // ArithmeticException if b is 0 (unchecked)
}
```

### Common Exception Types

| Python | Java |
|--------|------|
| `ValueError` | `IllegalArgumentException` |
| `TypeError` | `ClassCastException` |
| `IndexError` | `ArrayIndexOutOfBoundsException` |
| `KeyError` | `NoSuchElementException` |
| `FileNotFoundError` | `FileNotFoundException` (checked) |
| `IOError` | `IOException` (checked) |

### Try-with-Resources

Java 7+ has automatic resource management (similar to Python's `with`):

**Python:**
```python
with open("file.txt") as f:
    content = f.read()
# File automatically closed
```

**Java:**
```java
try (FileReader reader = new FileReader("file.txt")) {
    // Use reader
}  // Automatically closed, even if exception occurs
```

---

[← Previous: Custom Types](08-custom-types.md) | [Back to Java Guide](README.md)
