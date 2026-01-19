# Java Reading Guide by Phase

This guide maps the Python-to-Java reference materials to the course phases. Read the assigned sections **before** watching the async videos—they'll provide context and help you recognize familiar patterns.

---

## Phase 1: Basics (Session 1 Async)

**Topics:** Variables, types, I/O, operators, basic classes

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [01-basics](01-basics.md) | All | Hello World, System.out, Scanner, variables |
| [02-data-types](02-data-types.md) | All | int, double, String, boolean, type conversion |
| [03-operators](03-operators.md) | All | Arithmetic, comparison, logical (&&, \|\|, !) |

**Time estimate:** ~20 minutes

**Key takeaways:**
- Every variable needs a type declaration
- Use `System.out.println()` instead of `print()`
- Use `Scanner` for input instead of `input()`
- Semicolons are required after every statement
- Use `&&`, `||`, `!` instead of `and`, `or`, `not`
- Strings use `.equals()` for comparison, not `==`

---

## Phase 2: Collections (Session 3-4)

**Topics:** ArrayList, HashMap, iteration, file I/O

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [04-control-flow](04-control-flow.md) | All | if/else, for loops, enhanced for loop |
| [05-data-structures](05-data-structures.md) | All | ArrayList, HashMap, Strings, File I/O |

**Time estimate:** ~25 minutes

**Key takeaways:**
- `ArrayList<Integer>` is like Python's list (but uses wrapper types)
- Use `add()` instead of `append()`, `size()` instead of `len()`
- Enhanced for loop: `for (int x : list)` is like `for x in list`
- Use `BufferedReader` or `Scanner` for file reading
- Try-with-resources (`try (...)`) auto-closes files like Python's `with`

---

## Phase 3: OOP (Session 5-7)

**Topics:** Classes, constructors, inheritance, interfaces

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [06-functions](06-functions.md) | All | Methods, parameters, return types, overloading |
| [07-oop](07-oop.md) | All | Classes, access modifiers, inheritance, interfaces |

**Time estimate:** ~25 minutes

**Key takeaways:**
- Constructor has the same name as the class (no `__init__`)
- Use `this` instead of `self` (and it's optional in most cases)
- Access modifiers (`public`, `private`) are enforced by compiler
- Java uses `extends` for inheritance (single inheritance only)
- Use `implements` for interfaces (Java's answer to multiple inheritance)
- Always use `@Override` annotation when overriding methods

---

## Phase 4: Unique Features (Session 8)

**Topics:** Exception handling, packages, static members

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [08-unique-features](08-unique-features.md) | All | Exceptions, packages, static, final |

**Time estimate:** ~20 minutes

**Key takeaways:**
- Use `try/catch` blocks for exception handling
- `throws` declares exceptions a method might throw
- `static` members belong to the class, not instances
- `final` means constant (like Python's convention for `CONSTANTS`)
- Package structure mirrors directory structure

---

## Quick Reference: What to Read When

| Phase | Session | Read Before Class |
|-------|---------|-------------------|
| 1 | S1 (Mon) | 01-basics, 02-data-types, 03-operators |
| 2 | S3 (Mon) | 04-control-flow, 05-data-structures |
| 3 | S5 (Mon) | 06-functions, 07-oop |
| 4 | S8 (Wed) | 08-unique-features |

---

## Full Reference

For complete coverage or later review, all sections are available:

| Guide | Topics |
|-------|--------|
| [01-basics](01-basics.md) | Hello World, I/O, variables, constants |
| [02-data-types](02-data-types.md) | Types, wrapper classes, type conversion |
| [03-operators](03-operators.md) | Arithmetic, comparison, logical |
| [04-control-flow](04-control-flow.md) | If/else, for, while, switch |
| [05-data-structures](05-data-structures.md) | ArrayList, HashMap, Strings, File I/O |
| [06-functions](06-functions.md) | Methods, parameters, overloading |
| [07-oop](07-oop.md) | Classes, inheritance, interfaces |
| [08-unique-features](08-unique-features.md) | Exceptions, packages, static, final |
