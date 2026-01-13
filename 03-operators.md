# 03 - Operators

[← Back to Java Guide](README.md)

Most operators work the same in Java as in Python, but there are a few important differences. The biggest gotcha is integer division: `7 / 2` gives `3` in Java (not `3.5`). Java also uses symbols for logical operators (`&&`, `||`, `!`) instead of words (`and`, `or`, `not`), and there's no `**` operator for exponents—use `Math.pow()` instead.

---

## Arithmetic

| Operation | Python | Java |
|-----------|--------|------|
| Addition | `a + b` | `a + b` |
| Subtraction | `a - b` | `a - b` |
| Multiplication | `a * b` | `a * b` |
| Division | `a / b` (float result) | `a / b` (int if both int!) |
| Floor division | `a // b` | `a / b` (for integers) |
| Modulus | `a % b` | `a % b` |
| Exponent | `a ** b` | `Math.pow(a, b)` |

## Important: Integer Division

This is a common gotcha when moving from Python to Java:

**Python:**
```python
7 / 2   # = 3.5 (always float)
7 // 2  # = 3 (floor division)
```

**Java:**
```java
7 / 2     // = 3 (integer division!)
7.0 / 2   // = 3.5 (float division)
(double) 7 / 2  // = 3.5 (cast to force float division)
```

In Java, if both operands are integers, `/` performs integer division. To get a float result, at least one operand must be a float/double.

## Increment and Decrement

Java has `++` and `--` operators that Python doesn't have:

```java
int x = 5;
x++;        // x is now 6 (same as x = x + 1)
x--;        // x is now 5 (same as x = x - 1)

// Pre vs Post increment
int a = 5;
int b = a++;   // b = 5, a = 6 (assign first, then increment)
int c = ++a;   // c = 7, a = 7 (increment first, then assign)
```

## Compound Assignment

| Python | Java |
|--------|------|
| `x += 1` | `x += 1;` |
| `x -= 1` | `x -= 1;` |
| `x *= 2` | `x *= 2;` |
| `x /= 2` | `x /= 2;` |

## Comparison

| Operation | Python | Java |
|-----------|--------|------|
| Equal | `==` | `==` (primitives) or `.equals()` (objects) |
| Not equal | `!=` | `!=` (primitives) or `!.equals()` (objects) |
| Less than | `<` | `<` |
| Greater than | `>` | `>` |
| Less or equal | `<=` | `<=` |
| Greater or equal | `>=` | `>=` |

### Important: Comparing Objects

For **primitives**, use `==`:
```java
int a = 5;
int b = 5;
if (a == b) { }  // true - comparing values
```

For **objects** (including Strings), use `.equals()`:
```java
String s1 = "hello";
String s2 = "hello";
if (s1 == s2) { }       // Compares references (may or may not work!)
if (s1.equals(s2)) { }  // Compares content (correct way!)
```

## Logical

| Operation | Python | Java |
|-----------|--------|------|
| And | `and` | `&&` |
| Or | `or` | `\|\|` |
| Not | `not` | `!` |

**Python:**
```python
if x > 0 and y > 0:
    print("Both positive")
if not found:
    print("Not found")
```

**Java:**
```java
if (x > 0 && y > 0) {
    System.out.println("Both positive");
}
if (!found) {
    System.out.println("Not found");
}
```

## String Concatenation

Java uses `+` for string concatenation (like Python):

```java
String first = "Hello";
String second = "World";
String message = first + " " + second;  // "Hello World"

// Mixing strings and numbers
int age = 25;
String info = "Age: " + age;  // "Age: 25" (auto-converts int to string)
```

---

[← Previous: Data Types](02-data-types.md) | [Next: Control Flow →](04-control-flow.md)
