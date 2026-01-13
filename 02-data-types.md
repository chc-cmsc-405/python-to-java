# 02 - Data Types

[← Back to Java Guide](README.md)

Java is statically typed—every variable must have a declared type, and that type cannot change. Java distinguishes between **primitive types** (basic values like `int`, `double`, `boolean`) and **reference types** (objects like `String`, arrays, custom classes). Primitives are stored directly in memory, while reference types store a reference to an object on the heap.

---

## Primitive Types

Java has 8 primitive types. These are the most common:

| Concept | Python | Java |
|---------|--------|------|
| **Integer** | `x = 42` | `int x = 42;` |
| **Long integer** | `x = 42` (same) | `long x = 42L;` |
| **Float** | `x = 3.14` | `double x = 3.14;` or `float x = 3.14f;` |
| **Boolean** | `True`, `False` | `true`, `false` |
| **Character** | `'a'` (just a string) | `char c = 'a';` (distinct type) |

**All primitive types:**

| Type | Size | Range | Default |
|------|------|-------|---------|
| `byte` | 8 bits | -128 to 127 | 0 |
| `short` | 16 bits | -32,768 to 32,767 | 0 |
| `int` | 32 bits | -2B to 2B | 0 |
| `long` | 64 bits | Very large | 0L |
| `float` | 32 bits | ~7 decimal digits | 0.0f |
| `double` | 64 bits | ~15 decimal digits | 0.0 |
| `boolean` | 1 bit | true/false | false |
| `char` | 16 bits | Unicode character | '\u0000' |

## Reference Types

Everything else in Java is a reference type: `String`, arrays, collections, custom classes.

**Python:**
```python
name = "Alice"     # String
numbers = [1,2,3]  # List (reference type)
```

**Java:**
```java
String name = "Alice";           // Reference type
int[] numbers = {1, 2, 3};       // Array (reference type)
ArrayList<Integer> list = new ArrayList<>();  // Collection
```

## Wrapper Classes (Primitives vs Objects)

Java provides wrapper classes that turn primitives into objects. This matters for collections, which can only hold objects.

| Primitive | Wrapper Class |
|-----------|---------------|
| `int` | `Integer` |
| `double` | `Double` |
| `boolean` | `Boolean` |
| `char` | `Character` |
| `long` | `Long` |
| `float` | `Float` |

**Why wrappers exist:**
```java
// Collections require objects, not primitives
ArrayList<int> list;        // ERROR!
ArrayList<Integer> list;    // OK - uses wrapper class

// Autoboxing: Java converts automatically
Integer num = 42;           // int → Integer (autoboxing)
int x = num;                // Integer → int (unboxing)
```

## Strings

Strings in Java are objects, not primitives. They are immutable (cannot be changed after creation).

**Python:**
```python
s = "Hello"
s = 'Hello'      # Same thing
```

**Java:**
```java
String s = "Hello";    // String literal (preferred)
String s = new String("Hello");  // Object creation (rarely needed)
```

## Null

Java uses `null` instead of Python's `None`:

| Python | Java |
|--------|------|
| `x = None` | `String x = null;` |
| `if x is None:` | `if (x == null)` |
| `if x is not None:` | `if (x != null)` |

**Important:** Only reference types can be null. Primitives cannot be null.

```java
String name = null;    // OK - reference type
int x = null;          // ERROR - primitive cannot be null
Integer y = null;      // OK - wrapper class is a reference type
```

## Type Conversion

| Python | Java |
|--------|------|
| `int("42")` | `Integer.parseInt("42")` |
| `float("3.14")` | `Double.parseDouble("3.14")` |
| `str(42)` | `String.valueOf(42)` or `Integer.toString(42)` |
| `int(3.7)` → `3` | `(int) 3.7` |

**Python:**
```python
num_str = "42"
num = int(num_str)      # String to int
pi = float("3.14")      # String to float
text = str(100)         # Int to string
```

**Java:**
```java
String numStr = "42";
int num = Integer.parseInt(numStr);        // String to int
double pi = Double.parseDouble("3.14");    // String to double
String text = String.valueOf(100);         // Int to string
String text2 = "" + 100;                   // Shortcut: concat with empty string
```

---

[← Previous: Basics](01-basics.md) | [Next: Operators →](03-operators.md)
