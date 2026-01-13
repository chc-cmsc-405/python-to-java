# 07 - Object-Oriented Programming

[← Back to Java Guide](README.md)

Java is a strictly object-oriented language—everything must be inside a class. Unlike Python where OOP is optional, Java enforces it from the start. Classes have explicit access modifiers (`public`, `private`, `protected`) that the compiler enforces. Constructors have the same name as the class instead of `__init__`, and there's no `self` parameter—the `this` keyword is used to refer to the current object.

---

## Class Definition

**Python:**
```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        print(f"{self.name} says woof!")

    def get_age(self):
        return self.age
```

**Java:**
```java
public class Dog {
    private String name;
    private int age;

    // Constructor
    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void bark() {
        System.out.println(name + " says woof!");
    }

    public int getAge() {
        return age;
    }
}
```

## Creating Objects

**Python:**
```python
my_dog = Dog("Buddy", 3)
my_dog.bark()
print(my_dog.get_age())
```

**Java:**
```java
Dog myDog = new Dog("Buddy", 3);
myDog.bark();
System.out.println(myDog.getAge());
```

**Note:** Java requires the `new` keyword to create objects.

## Key OOP Differences

| Concept | Python | Java |
|---------|--------|------|
| **Constructor** | `def __init__(self):` | `public ClassName() { }` |
| **Self reference** | `self` (explicit parameter) | `this` (implicit keyword) |
| **Access modifiers** | Convention only (`_private`) | `public`, `private`, `protected` |
| **Inheritance** | `class Child(Parent):` | `class Child extends Parent { }` |
| **Multiple inheritance** | Supported | Not supported (use interfaces) |
| **Create object** | `obj = MyClass()` | `MyClass obj = new MyClass();` |

## Access Modifiers

Python uses naming conventions. Java enforces access:

**Python:**
```python
class Person:
    def __init__(self, name):
        self.name = name       # Public (convention)
        self._age = 0          # "Private" (convention only)
        self.__secret = "x"    # Name-mangled
```

**Java:**
```java
public class Person {
    public String name;        // Accessible from anywhere
    private int age;           // Only accessible within class
    protected String secret;   // Accessible in class and subclasses
    String status;             // Package-private (no modifier)
}
```

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| `public` | Yes | Yes | Yes | Yes |
| `protected` | Yes | Yes | Yes | No |
| (none) | Yes | Yes | No | No |
| `private` | Yes | No | No | No |

## Getters and Setters

Java conventionally uses getter/setter methods for private fields:

**Python:**
```python
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, value):
        self._name = value
```

**Java:**
```java
public class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

## Inheritance

**Python:**
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print(f"{self.name} says woof!")
```

**Java:**
```java
public class Animal {
    protected String name;

    public Animal(String name) {
        this.name = name;
    }

    public void speak() {
        // Base implementation (or make abstract)
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);  // Call parent constructor
    }

    @Override
    public void speak() {
        System.out.println(name + " says woof!");
    }
}
```

## Interfaces

Java uses interfaces instead of multiple inheritance:

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

## Using `this`

**Python:**
```python
class Counter:
    def __init__(self):
        self.count = 0

    def increment(self):
        self.count += 1
        return self  # Method chaining
```

**Java:**
```java
public class Counter {
    private int count;

    public Counter() {
        this.count = 0;
    }

    public Counter increment() {
        this.count++;
        return this;  // Method chaining
    }
}
```

---

[← Previous: Functions](06-functions.md) | [Next: Unique Features →](08-unique-features.md)
