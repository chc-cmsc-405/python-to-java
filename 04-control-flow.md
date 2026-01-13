# 04 - Control Flow

[← Back to Java Guide](README.md)

Control structures in Java follow the same logic as Python but with different syntax. Conditions must be wrapped in parentheses, and code blocks use braces instead of indentation. Python's `elif` becomes `else if`. Java also has a `switch` statement for multiple conditions on a single value, and a `do-while` loop that guarantees at least one iteration.

---

## If / Else

**Python:**
```python
if x > 0:
    print("Positive")
elif x < 0:
    print("Negative")
else:
    print("Zero")
```

**Java:**
```java
if (x > 0) {
    System.out.println("Positive");
} else if (x < 0) {
    System.out.println("Negative");
} else {
    System.out.println("Zero");
}
```

**Key differences:**
- Java requires parentheses `()` around the condition
- Java uses braces `{}` instead of indentation
- `elif` becomes `else if`

## Ternary Operator

| Python | Java |
|--------|------|
| `result = "yes" if x > 0 else "no"` | `String result = (x > 0) ? "yes" : "no";` |

## Switch Statement

Java has a `switch` statement that Python doesn't have (until Python 3.10's `match`):

**Python (3.10+):**
```python
match grade:
    case 'A':
        print("Excellent")
    case 'B':
        print("Good")
    case _:
        print("Unknown")
```

**Java (traditional):**
```java
switch (grade) {
    case 'A':
        System.out.println("Excellent");
        break;
    case 'B':
        System.out.println("Good");
        break;
    default:
        System.out.println("Unknown");
}
```

**Java 14+ (enhanced switch):**
```java
switch (grade) {
    case 'A' -> System.out.println("Excellent");
    case 'B' -> System.out.println("Good");
    default -> System.out.println("Unknown");
}
```

## For Loop

**Python:**
```python
# Range-based
for i in range(5):
    print(i)

# With start and end
for i in range(1, 10):
    print(i)

# Iterating over list
for item in my_list:
    print(item)
```

**Java:**
```java
// Traditional for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// With start and end
for (int i = 1; i < 10; i++) {
    System.out.println(i);
}

// Enhanced for loop (for-each)
for (int item : myList) {
    System.out.println(item);
}
```

## While Loop

**Python:**
```python
while x > 0:
    print(x)
    x -= 1
```

**Java:**
```java
while (x > 0) {
    System.out.println(x);
    x--;
}
```

## Do-While Loop

Java has a do-while loop that Python doesn't have. It executes at least once before checking the condition:

```java
// Executes at least once
do {
    System.out.println(x);
    x--;
} while (x > 0);
```

This is useful when you need to execute code at least once (like menu prompts).

## Break and Continue

Same keywords in both languages: `break` and `continue`

**Python:**
```python
for i in range(10):
    if i == 5:
        break       # Exit loop
    if i % 2 == 0:
        continue    # Skip to next iteration
    print(i)
```

**Java:**
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;      // Exit loop
    }
    if (i % 2 == 0) {
        continue;   // Skip to next iteration
    }
    System.out.println(i);
}
```

## Labeled Break (Java-specific)

Java can break out of nested loops using labels:

```java
outer:
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        if (i * j > 50) {
            break outer;  // Breaks out of both loops
        }
    }
}
```

---

[← Previous: Operators](03-operators.md) | [Next: Data Structures →](05-data-structures.md)
