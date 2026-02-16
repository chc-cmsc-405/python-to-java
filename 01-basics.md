# 01 - Basics

[← Back to Java Guide](README.md)

Every Java program needs a `main` method inside a class as its entry point—unlike Python where code runs from the top of the file. The class name must match the filename exactly (`HelloWorld.java` contains `class HelloWorld`). The basic syntax will feel familiar, but pay attention to semicolons (required after every statement) and braces (used instead of indentation for code blocks).

---

## Comments

| Python | Java |
|--------|------|
| `# Single line comment` | `// Single line comment` |
| `""" Multi-line comment """` | `/* Multi-line comment */` |

Java also has **Javadoc comments** for documentation:
```java
/**
 * This is a Javadoc comment
 * @param name The name to greet
 * @return A greeting message
 */
```

## Hello World

**Python:**
```python
print("Hello, World!")
```

**Java:**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Key points:**
- Class name must match filename (`HelloWorld.java`)
- `public static void main(String[] args)` is the exact signature required
- `System.out.println()` adds a newline; `System.out.print()` does not

## Console Output

| Python | Java |
|--------|------|
| `print(value)` | `System.out.println(value);` |
| `print(a, b, c)` | `System.out.println(a + " " + b + " " + c);` |
| `print(f"Value: {x}")` | `System.out.println("Value: " + x);` |
| `print("hi", end="")` | `System.out.print("hi");` |

**Formatted output (printf):**
```java
System.out.printf("Name: %s, Age: %d%n", name, age);
System.out.printf("Price: %.2f%n", price);  // 2 decimal places
```

## Console Input

Java requires creating a `Scanner` object to read console input:

**Python:**
```python
name = input("Enter name: ")
age = int(input("Enter age: "))
```

**Java:**
```java
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter name: ");
        String name = scanner.nextLine();

        System.out.print("Enter age: ");
        int age = scanner.nextInt();

        scanner.close();
    }
}
```

**Scanner methods:**

| Input Type | Method |
|------------|--------|
| String (full line) | `scanner.nextLine()` |
| String (word) | `scanner.next()` |
| Integer | `scanner.nextInt()` |
| Double | `scanner.nextDouble()` |
| Boolean | `scanner.nextBoolean()` |

## Variables

**Python:**
```python
x = 10          # No type declaration
name = "Alice"  # Type inferred
pi = 3.14       # Type inferred
```

**Java:**
```java
int x = 10;              // Type required
String name = "Alice";   // Type required
double pi = 3.14;        // Type required
var y = 20;              // Type inference (Java 10+)
```

## Constants

| Python | Java |
|--------|------|
| `PI = 3.14159` (convention only) | `final double PI = 3.14159;` |
| No true constants | `static final int MAX = 100;` |

**Java:**
```java
public class Constants {
    // Class-level constant
    public static final double PI = 3.14159;

    public static void main(String[] args) {
        // Local constant
        final int MAX_SIZE = 100;
        // MAX_SIZE = 200;  // Error! Cannot reassign final variable
    }
}
```

## The main Method Explained

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
```

| Python | Java |
|--------|------|
| `from math import sqrt` | `import java.lang.Math;` (Math auto-imported) |
| `import os` | `import java.io.*;` |
| `from collections import defaultdict` | `import java.util.HashMap;` |

## Compilation

Unlike Python's immediate execution, Java compiles to **bytecode** that runs on the JVM:

```
Java Source (.java) → Compiler → Bytecode (.class) → JVM → Execution
```

```bash
# Compile source to bytecode
javac HelloWorld.java

# Run the bytecode on JVM
java HelloWorld
```

**Benefits of the JVM:**
- **Portability:** Same bytecode runs on any platform with a JVM
- **Memory management:** Automatic garbage collection
- **Security:** JVM provides a sandbox environment

---

[Next: Data Types →](02-data-types.md)
