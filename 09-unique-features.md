# 09 - Java Unique Features

[← Back to Java Guide](README.md)

These concepts don't have direct Python equivalents or work significantly differently. Java runs on the JVM (Java Virtual Machine), enabling "write once, run anywhere." Packages organize code into namespaces. Exception handling is more structured, with checked exceptions requiring explicit handling. Access modifiers give fine-grained control over visibility.

---

## The JVM (Java Virtual Machine)

Unlike Python (interpreted) or C++ (compiled to machine code), Java compiles to **bytecode** that runs on the JVM:

```
Java Source (.java) → Compiler → Bytecode (.class) → JVM → Execution
```

**Benefits:**
- **Portability:** Same bytecode runs on any platform with a JVM
- **Security:** JVM provides a sandbox environment
- **Memory management:** Automatic garbage collection

**Compilation and execution:**
```bash
# Compile source to bytecode
javac HelloWorld.java

# Run the bytecode on JVM
java HelloWorld
```

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

## Packages and Imports

Java uses packages to organize classes and avoid naming conflicts:

**Package declaration (at top of file):**
```java
package com.example.myapp;

public class MyClass {
    // ...
}
```

**Importing classes:**
```java
import java.util.ArrayList;       // Import specific class
import java.util.HashMap;
import java.util.*;               // Import all classes from package (not recommended)

// Or use fully qualified name without import
java.util.ArrayList<String> list = new java.util.ArrayList<>();
```

**Comparison to Python:**

| Python | Java |
|--------|------|
| `from math import sqrt` | `import java.lang.Math;` (Math auto-imported) |
| `import os` | `import java.io.*;` |
| `from collections import defaultdict` | `import java.util.HashMap;` |

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

## Static Members

The `static` keyword creates class-level variables and methods (shared across all instances):

```java
public class Counter {
    private static int totalCount = 0;  // Shared across all instances
    private int instanceCount = 0;       // Unique to each instance

    public Counter() {
        totalCount++;
        instanceCount++;
    }

    public static int getTotalCount() {  // Can call without object
        return totalCount;
    }
}

// Usage
Counter c1 = new Counter();
Counter c2 = new Counter();
System.out.println(Counter.getTotalCount());  // 2 (called on class)
```

## Final Keyword

`final` has multiple uses in Java:

```java
// Final variable (constant)
final double PI = 3.14159;

// Final method (cannot be overridden)
public final void importantMethod() { }

// Final class (cannot be extended)
public final class String { }  // String is actually final in Java
```

## The `main` Method Explained

Every Java program needs this exact signature:

```java
public static void main(String[] args) {
    // Program starts here
}
```

| Part | Meaning |
|------|---------|
| `public` | Accessible from anywhere (JVM needs to call it) |
| `static` | Belongs to class, not instance (no object needed to start) |
| `void` | Returns nothing |
| `main` | Exact name JVM looks for |
| `String[] args` | Command-line arguments |

**Accessing command-line arguments:**
```java
public static void main(String[] args) {
    if (args.length > 0) {
        System.out.println("First argument: " + args[0]);
    }
}
```

---

[← Previous: Custom Types](08-custom-types.md) | [Back to Java Guide](README.md)
