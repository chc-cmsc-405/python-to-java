# Java For Python Programmers

You already know Python. This guide helps you learn Java by showing side-by-side comparisons with familiar Python syntax.

## How to Use This Guide

- **[Reading Guide](reading-guide.md)** — Phase-aligned reading assignments for CMSC-405
- **Quick Reference** — This README has dense comparison tables for quick lookup
- **Deep Dive** — Individual pages (linked below) cover specific topics in detail with code examples
- **Side-by-Side** — Python code on the left, Java on the right

---

## About Java

Java is an object-oriented programming language designed around the principle of "write once, run anywhere." Code compiles to bytecode that runs on the Java Virtual Machine (JVM), which is available on virtually every platform. Java is widely used in enterprise applications, Android development, web backends, and large-scale systems. Unlike C++, Java handles memory automatically through garbage collection. The syntax will feel familiar—both languages share C-style structure—but Java requires everything to live inside a class, making it more strictly object-oriented than Python.

---

## Key Differences

Java is a statically-typed, compiled language that runs on the JVM. Unlike Python where you can just run your code, Java requires compilation to bytecode. You must declare variable types, use braces for code blocks, and end statements with semicolons. Everything in Java must be inside a class.

| Aspect | Python | Java |
|--------|--------|------|
| **Typing** | Dynamic | Static (declare types) |
| **Execution** | Interpreted | Compiled to bytecode (JVM) |
| **Memory** | Garbage collected | Garbage collected |
| **Blocks** | Indentation | Braces `{ }` |
| **Semicolons** | Not required | Required |
| **Main function** | Optional | Required: `public static void main(String[] args)` |
| **Structure** | Functions anywhere | Everything inside a class |

---

## Quick Reference

### Output & Input

Java uses `System.out.println()` for output and `Scanner` for input. Unlike Python's simple `print()` and `input()`, Java requires more setup for reading user input.

| Task | Python | Java |
|------|--------|------|
| Print | `print("hi")` | `System.out.println("hi");` |
| Print variable | `print(x)` | `System.out.println(x);` |
| Print without newline | `print("hi", end="")` | `System.out.print("hi");` |
| Formatted print | `print(f"Value: {x}")` | `System.out.println("Value: " + x);` |

### Variables & Constants

In Java, you must declare the type of every variable. The compiler uses this information to catch errors. Use `final` to create constants that cannot be changed after initialization.

| Task | Python | Java |
|------|--------|------|
| Integer | `x = 5` | `int x = 5;` |
| Float | `x = 3.14` | `double x = 3.14;` |
| String | `s = "hello"` | `String s = "hello";` |
| Boolean | `flag = True` | `boolean flag = true;` |
| Constant | `PI = 3.14` | `final double PI = 3.14;` |

### Control Flow

Control structures work similarly, but Java requires parentheses around conditions and braces around code blocks. Python's `elif` becomes `else if` in Java.

| Task | Python | Java |
|------|--------|------|
| If | `if x > 0:` | `if (x > 0) {` |
| Else if | `elif x < 0:` | `} else if (x < 0) {` |
| Else | `else:` | `} else {` |
| Ternary | `"yes" if x else "no"` | `x ? "yes" : "no"` |

### Loops

Java uses the traditional three-part `for` loop with initialization, condition, and increment. The enhanced `for` loop is similar to Python's `for-each` pattern.

| Task | Python | Java |
|------|--------|------|
| For (range) | `for i in range(5):` | `for (int i = 0; i < 5; i++) {` |
| For (each) | `for x in items:` | `for (int x : items) {` |
| While | `while x > 0:` | `while (x > 0) {` |

### Functions (Methods)

In Java, all functions are methods inside a class. They require explicit return types and parameter types. Use `void` if no return value. The `static` keyword means the method belongs to the class, not an instance.

| Task | Python | Java |
|------|--------|------|
| Define | `def foo():` | `public static void foo() {` |
| With return | `def add(a, b): return a + b` | `public static int add(int a, int b) { return a + b; }` |
| No return | `def greet():` | `public static void greet() {` |

### Data Structures

Java's `ArrayList` is similar to Python's list—a resizable array. Unlike Python lists, Java collections require a type parameter. `HashMap` works like Python dictionaries.

| Task | Python | Java |
|------|--------|------|
| List | `[1, 2, 3]` | `ArrayList<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));` |
| Append | `list.append(x)` | `list.add(x);` |
| Access | `list[0]` | `list.get(0)` |
| Length | `len(list)` | `list.size()` |
| Dictionary | `{"a": 1}` | `HashMap<String, Integer> map = new HashMap<>();` |

### Classes

Java is strictly object-oriented—every piece of code lives inside a class. Access modifiers (`public`, `private`) are enforced by the compiler. Constructors have the same name as the class.

| Task | Python | Java |
|------|--------|------|
| Define | `class Dog:` | `public class Dog { }` |
| Constructor | `def __init__(self):` | `public Dog() { }` |
| Method | `def bark(self):` | `public void bark() {` |
| Create object | `d = Dog()` | `Dog d = new Dog();` |

### Operators & Comments

Most operators are identical. Division between integers gives an integer result. Logical operators use symbols instead of words.

| Task | Python | Java |
|------|--------|------|
| And / Or / Not | `and` `or` `not` | `&&` `\|\|` `!` |
| Exponent | `x ** 2` | `Math.pow(x, 2)` |
| Integer division | `7 // 2` → `3` | `7 / 2` → `3` |
| Float division | `7 / 2` → `3.5` | `7.0 / 2` → `3.5` |
| Comment | `# comment` | `// comment` |
| Multi-line | `""" comment """` | `/* comment */` |

---

## Common Imports

Java uses `import` statements to bring in library classes. These are the imports you'll use most often:

```java
import java.util.Scanner;       // User input
import java.util.ArrayList;     // Resizable arrays
import java.util.HashMap;       // Key-value pairs
import java.util.Arrays;        // Array utilities
import java.lang.Math;          // Math functions (auto-imported)
```

---

## Detailed Sections

For more examples and in-depth explanations, see:

| Section | Topics |
|---------|--------|
| [01 - Basics](01-basics.md) | Comments, Hello World, console I/O, variables, constants |
| [02 - Data Types](02-data-types.md) | Primitives, wrapper classes, type conversion |
| [03 - Operators](03-operators.md) | Arithmetic, comparison, logical |
| [04 - Control Flow](04-control-flow.md) | If/else, for, while, switch |
| [05 - Functions](05-functions.md) | Methods, parameters, return types, overloading |
| [06 - Data Structures](06-data-structures.md) | Arrays, ArrayList, HashMap, Strings |
| [07 - I/O Streams](07-io-streams.md) | File I/O, BufferedReader, PrintWriter, CSV parsing |
| [08 - Custom Types](08-custom-types.md) | Classes, constructors, inheritance, interfaces |
| [09 - Unique Features](09-unique-features.md) | JVM, packages, exceptions, access modifiers |

---

*This guide covers the basics. Java has many more features that you'll learn throughout the course.*
