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

---

## Wrapper Classes

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

**Wrapper class methods:**

| Task | Code |
|------|------|
| Parse string to int | `Integer.parseInt("42")` |
| Parse string to double | `Double.parseDouble("3.14")` |
| Int to string | `Integer.toString(42)` |
| Max int value | `Integer.MAX_VALUE` |
| Compare | `Integer.compare(a, b)` |

---

## Strings

Strings in Java are objects, not primitives. They are **immutable**—methods return new strings, they don't modify the original.

### String Basics

| Concept | Python | Java |
|---------|--------|------|
| **Create** | `s = "hello"` | `String s = "hello";` |
| **Length** | `len(s)` | `s.length()` |
| **Concatenate** | `s1 + s2` | `s1 + s2` |
| **Access char** | `s[0]` | `s.charAt(0)` |
| **Check empty** | `if not s:` | `if (s.isEmpty())` |
| **Uppercase** | `s.upper()` | `s.toUpperCase()` |
| **Lowercase** | `s.lower()` | `s.toLowerCase()` |
| **Strip whitespace** | `s.strip()` | `s.trim()` |
| **Split** | `s.split(",")` | `s.split(",")` |

### String Operations (Finding & Extracting)

| Concept | Python | Java |
|---------|--------|------|
| **Find** | `s.find("ell")` | `s.indexOf("ell")` |
| **Find from end** | `s.rfind("l")` | `s.lastIndexOf("l")` |
| **Substring** | `s[1:4]` | `s.substring(1, 4)` (start, end) |
| **Contains** | `"ell" in s` | `s.contains("ell")` |
| **Starts with** | `s.startswith("He")` | `s.startsWith("He")` |
| **Ends with** | `s.endswith("!")` | `s.endsWith("!")` |

```java
String text = "Hello, World!";
System.out.println(text.indexOf("o"));        // 4
System.out.println(text.lastIndexOf("o"));    // 8
System.out.println(text.substring(0, 5));     // Hello
System.out.println(text.startsWith("Hello")); // true
```

### String Modifiers

| Concept | Python | Java |
|---------|--------|------|
| **Replace all** | `s.replace("o", "0")` | `s.replace("o", "0")` |
| **Replace first** | N/A | `s.replaceFirst("o", "0")` |
| **Join** | `",".join(list)` | `String.join(",", list)` |

```java
String text = "Hello, World!";
System.out.println(text.replace("o", "0"));      // Hell0, W0rld!
System.out.println(text.replaceFirst("o", "0")); // Hell0, World!
// Original 'text' is unchanged
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

## Character Functions

Java provides character functions in the `Character` class. In Python, these are methods on strings. In Java, they're static methods that take a character.

| Task | Python | Java |
|------|--------|------|
| **Is letter?** | `c.isalpha()` | `Character.isLetter(c)` |
| **Is digit?** | `c.isdigit()` | `Character.isDigit(c)` |
| **Is alphanumeric?** | `c.isalnum()` | `Character.isLetterOrDigit(c)` |
| **Is whitespace?** | `c.isspace()` | `Character.isWhitespace(c)` |
| **Is uppercase?** | `c.isupper()` | `Character.isUpperCase(c)` |
| **Is lowercase?** | `c.islower()` | `Character.isLowerCase(c)` |
| **To uppercase** | `c.upper()` | `Character.toUpperCase(c)` |
| **To lowercase** | `c.lower()` | `Character.toLowerCase(c)` |

**Python:**
```python
text = "Hello123"
for c in text:
    if c.isalpha():
        print(c.upper())
    elif c.isdigit():
        print(c)
```

**Java:**
```java
String text = "Hello123";
for (char c : text.toCharArray()) {
    if (Character.isLetter(c)) {
        System.out.print(Character.toUpperCase(c));
    } else if (Character.isDigit(c)) {
        System.out.print(c);
    }
}
```

---

## Type Conversions

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

---

[← Previous: Basics](01-basics.md) | [Next: Operators →](03-operators.md)
