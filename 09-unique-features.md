# 09 - Java Unique Features

[← Back to Java Guide](README.md)

These concepts don't have direct Python equivalents or work significantly differently in Java. Interfaces and abstract classes provide structure that Python leaves to convention. Exception handling is more rigid, with checked exceptions requiring explicit handling. Static and final keywords give you control over class-level behavior and immutability.

## Contents

- [Interfaces](#interfaces)
- [Abstract Classes](#abstract-classes)
- [Interfaces vs Abstract Classes](#interfaces-vs-abstract-classes)
- [Exception Handling](#exception-handling)
- [Static Members](#static-members)
- [Final Keyword](#final-keyword)
- [Memory Management: Python vs Java](#memory-management-python-vs-java)

---

## Interfaces

An interface defines a contract — a set of methods that a class promises to implement. Java uses interfaces where Python uses multiple inheritance or duck typing.

**Python:**
```python
class Flyable:
    def fly(self):
        pass

class Swimmable:
    def swim(self):
        pass

class Duck(Flyable, Swimmable):  # Multiple inheritance
    def fly(self):
        print("Flying")
    def swim(self):
        print("Swimming")
```

**Java:**
```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

public class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Flying");
    }

    @Override
    public void swim() {
        System.out.println("Swimming");
    }
}
```

Key concepts:

- **`interface`** — declares a contract with method signatures but no implementation. No fields (except constants), no constructors.
- **`implements`** — a class agrees to provide implementations for all methods in the interface.
- A class can implement **multiple interfaces** (unlike `extends`, which is limited to one parent class).
- Interfaces can be used as types: `Flyable f = new Duck();` — any class that implements Flyable can go here.

**When to use interfaces:** When unrelated classes need to share a capability. A `Duck` and an `Airplane` are nothing alike, but both can be `Flyable`.

## Abstract Classes

An abstract class sits between a regular class and an interface. It can have both implemented methods and abstract methods (methods with no body that subclasses must implement).

**Python:**
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def get_area(self):
        pass

    def describe(self):  # Concrete method
        print(f"Area: {self.get_area()}")
```

**Java:**
```java
public abstract class Shape {
    public abstract double getArea();  // No body — subclasses must implement

    public void describe() {  // Concrete method — inherited as-is
        System.out.println("Area: " + getArea());
    }
}

public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

Key concepts:

- **`abstract class`** — cannot be instantiated directly. `new Shape()` won't compile.
- **`abstract` methods** — declared with no body. Every non-abstract subclass must implement them.
- **Concrete methods** — regular methods with a body. Subclasses inherit them as-is (or can override them).
- A class can only extend **one** abstract class (same rule as regular inheritance).

## Interfaces vs Abstract Classes

| Feature | Interface | Abstract Class |
|---------|-----------|----------------|
| Methods | Abstract only (no body) | Mix of abstract and concrete |
| Fields | Constants only (`static final`) | Regular fields allowed |
| Constructor | No | Yes |
| Multiple | A class can implement many | A class can extend only one |
| Use when | Unrelated classes share a capability | Related classes share common behavior and state |

**Rule of thumb:** Use an interface when you're defining what something *can do*. Use an abstract class when you're defining what something *is* and sharing code between related classes.

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

### Custom Exceptions

You can create your own exception classes by extending `Exception` (checked) or `RuntimeException` (unchecked):

```java
public class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

// Throwing it
public void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) {
        throw new InsufficientFundsException("Balance: " + balance + ", requested: " + amount);
    }
    balance -= amount;
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

The `static` keyword creates class-level variables and methods that belong to the class itself, not to any instance. They're shared across all instances and can be called without creating an object.

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
System.out.println(Counter.getTotalCount());  // 2 (called on class, not instance)
```

**Python equivalent:** `@staticmethod` and `@classmethod` decorators, or class-level variables.

**Common uses:**
- Utility methods that don't need instance data (`Math.sqrt()`, `Integer.parseInt()`)
- Constants (`static final`)
- Factory methods
- Counters or shared state

## Final Keyword

`final` means "cannot be changed." It applies to variables, methods, and classes:

```java
// Final variable — constant, cannot be reassigned
final int MAX_SIZE = 100;

// Final field — must be set in constructor, cannot change after
public class Config {
    private final String name;

    public Config(String name) {
        this.name = name;  // Set once
    }
}

// Final method — cannot be overridden by subclasses
public final void criticalMethod() { }

// Final class — cannot be extended
public final class ImmutablePoint { }
```

**`static final`** is the standard pattern for constants in Java:

```java
public class MathConstants {
    public static final double PI = 3.14159265;
    public static final int MAX_RETRIES = 3;
}

// Usage
System.out.println(MathConstants.PI);
```

**Python equivalent:** Python has no `final`. Constants are by convention (ALL_CAPS names), but nothing prevents reassignment.

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

---

[← Previous: Custom Types](08-custom-types.md) | [Back to Java Guide](README.md)
