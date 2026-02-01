# 05 - Functions (Methods)

[← Back to Java Guide](README.md)

In Java, all functions are called **methods** and must live inside a class. They require explicit return types and parameter types. Use `void` if no return value. The `static` keyword means the method belongs to the class itself rather than an instance—you can call it without creating an object. Non-static methods (instance methods) require an object to call them on.

---

## Basic Method

**Python:**
```python
def greet(name):
    return f"Hello, {name}!"

message = greet("Alice")
```

**Java:**
```java
public class Example {
    public static String greet(String name) {
        return "Hello, " + name + "!";
    }

    public static void main(String[] args) {
        String message = greet("Alice");
    }
}
```

**Key difference:** In Java, you must declare the return type and parameter types.

## Method with Multiple Parameters

**Python:**
```python
def add(a, b):
    return a + b
```

**Java:**
```java
public static int add(int a, int b) {
    return a + b;
}
```

## Void Methods (No Return Value)

**Python:**
```python
def say_hello():
    print("Hello!")
    # No return statement needed
```

**Java:**
```java
public static void sayHello() {
    System.out.println("Hello!");
    // No return statement needed
}
```

## Static vs Instance Methods

This is a key Java concept with no direct Python equivalent:

**Static methods:** Called on the class, don't need an object
```java
public class Calculator {
    public static int add(int a, int b) {  // static method
        return a + b;
    }
}

// Call without creating object
int result = Calculator.add(5, 3);
```

**Instance methods:** Called on an object, can access instance variables
```java
public class Dog {
    private String name;

    public Dog(String name) {
        this.name = name;
    }

    public void bark() {  // instance method
        System.out.println(name + " says woof!");
    }
}

// Must create object first
Dog myDog = new Dog("Buddy");
myDog.bark();
```

## Method Overloading

Java supports **method overloading**—multiple methods with the same name but different parameters. Python doesn't have this.

**Java:**
```java
public class Calculator {
    // Same name, different parameter types
    public static int add(int a, int b) {
        return a + b;
    }

    public static double add(double a, double b) {
        return a + b;
    }

    // Same name, different number of parameters
    public static int add(int a, int b, int c) {
        return a + b + c;
    }
}

// Java chooses the right version based on arguments
Calculator.add(5, 3);       // Uses int version
Calculator.add(5.0, 3.0);   // Uses double version
Calculator.add(1, 2, 3);    // Uses three-parameter version
```

## Default Parameters

Java doesn't have default parameters like Python. Use method overloading instead:

**Python:**
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Alice")           # "Hello, Alice!"
greet("Alice", "Hi")     # "Hi, Alice!"
```

**Java (using overloading):**
```java
public static String greet(String name) {
    return greet(name, "Hello");  // Call overloaded version
}

public static String greet(String name, String greeting) {
    return greeting + ", " + name + "!";
}

greet("Alice");          // "Hello, Alice!"
greet("Alice", "Hi");    // "Hi, Alice!"
```

## Return Types

| Python | Java |
|--------|------|
| `def foo():` (any return type) | `void foo()` (no return) |
| `return 42` | `int foo() { return 42; }` |
| `return "hi"` | `String foo() { return "hi"; }` |
| `return [1,2]` | `int[] foo() { return new int[]{1,2}; }` |
| `return True` | `boolean foo() { return true; }` |

## Pass by Value vs Reference

In Python, the behavior depends on the type:
- **Immutable types** (`int`, `str`, `tuple`): Changes inside a function don't affect the original—similar to pass by value
- **Mutable types** (`list`, `dict`): Changes inside a function affect the original—similar to pass by reference

Java is **always pass-by-value**, but this can be confusing:

- **Primitives** (`int`, `double`, etc.): The value is copied. Changes don't affect the original.
- **Objects** (`ArrayList`, `String`, etc.): The reference is copied. The method can modify the object's contents, but can't reassign what the caller's variable points to.

This is similar to Python's behavior with mutable types.

```java
public static void modifyPrimitive(int x) {
    x = 100;  // Only changes local copy
}

public static void modifyList(ArrayList<Integer> list) {
    list.add(100);  // Modifies the actual list!
}

public static void main(String[] args) {
    int num = 5;
    modifyPrimitive(num);
    System.out.println(num);  // Still 5

    ArrayList<Integer> numbers = new ArrayList<>();
    modifyList(numbers);
    System.out.println(numbers.size());  // 1 (list was modified)
}
```

## The final Keyword

Java's `final` prevents reassignment, but it does NOT prevent modification of an object's contents:

```java
final int x = 10;
x = 20;  // Error! Can't reassign final variable

final ArrayList<Integer> list = new ArrayList<>();
list.add(1);           // OK - can still modify the list!
list = new ArrayList<>();  // Error - can't reassign to new list
```

**Note:** Unlike C++'s `const`, Java has no way to mark a parameter as "read-only" to prevent a method from modifying an object's contents. If you pass an `ArrayList` to a method, that method can always call `.add()` or `.remove()` on it.

---

[← Previous: Control Flow](04-control-flow.md) | [Next: Data Structures →](06-data-structures.md)
