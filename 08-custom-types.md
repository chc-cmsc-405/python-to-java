# 08 - Custom Types

[← Back to Java Guide](README.md)

Java is a strictly object-oriented language—everything must be inside a class. Unlike Python where OOP is optional, Java enforces it from the start. Classes have explicit access modifiers (`public`, `private`, `protected`) that the compiler enforces. Constructors have the same name as the class instead of `__init__`, and there's no `self` parameter—the `this` keyword is used to refer to the current object.

## Contents

- [Class Definition](#class-definition)
- [The this Keyword](#the-this-keyword)
- [Creating Objects](#creating-objects)
- [Key OOP Differences](#key-oop-differences)
- [Access Modifiers](#access-modifiers)
- [Getters and Setters](#getters-and-setters)
- [Inheritance](#inheritance)
- [Destructors: Not Needed](#destructors-not-needed)

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

Notice the pattern: fields are declared at the top of the class with access modifiers, the constructor initializes them, and methods provide access. Every field, constructor, and method has an explicit access level (`public` or `private`).

## The `this` Keyword

In Python, every method receives `self` as its first parameter — it's how you refer to the current object. Java uses `this` instead, but it works differently: `this` is implicit (not a parameter) and is only required when you need to disambiguate.

The most common use is in constructors where parameter names match field names:

```java
public class Dog {
    private String name;

    public Dog(String name) {
        this.name = name;  // this.name = the field, name = the parameter
    }
}
```

Without `this`, the compiler would think both `name` references mean the parameter. `this.name` says "the field belonging to this object."

In methods where there's no ambiguity, `this` is optional:

```java
public void bark() {
    System.out.println(name + " says woof!");  // no this needed
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

**Note:** Java requires the `new` keyword to create objects. The variable declaration includes the type (`Dog myDog`), and `new Dog(...)` calls the constructor and returns a reference to the new object.

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
class Dog:
    def __init__(self, name):
        self.name = name       # Public (convention)
        self._age = 0          # "Private" (convention only)
        self.__weight = 0.0    # Name-mangled
```

**Java:**
```java
public class Dog {
    public String name;        // Accessible from anywhere
    private int age;           // Only accessible within class
    protected double weight;   // Accessible in class and subclasses
    String breed;              // Package-private (no modifier)
}
```

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| `public` | Yes | Yes | Yes | Yes |
| `protected` | Yes | Yes | Yes | No |
| (none) | Yes | Yes | No | No |
| `private` | Yes | No | No | No |

The standard pattern is: fields are `private`, access goes through `public` getter/setter methods. This is called **encapsulation** — the class controls how its data is accessed and modified.

## Getters and Setters

Java conventionally uses getter/setter methods for private fields:

**Python:**
```python
class Dog:
    def __init__(self, name, age):
        self._name = name
        self._age = age

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, value):
        self._name = value
```

**Java:**
```java
public class Dog {
    private String name;
    private int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

The naming convention is `getFieldName()` and `setFieldName()`. Not every field needs a setter — `age` has a getter but no setter because a dog's age shouldn't be changed directly. This gives you control over what can be modified from outside the class.

## Inheritance

When multiple classes share common fields and behavior, you can pull the shared parts into a **base class** and have other classes **extend** it. The subclass inherits all the fields and methods of the parent, then adds its own.

**Why use inheritance?** Without it, you'd copy the same fields and methods into every class. With inheritance, shared fields and behavior live in one place — the base class.

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
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void speak() {
        // Base implementation
    }
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);  // Call parent constructor
    }

    @Override
    public void speak() {
        System.out.println(getName() + " says woof!");
    }
}
```

Key concepts:

- **`extends`** — declares that Dog is a subclass of Animal. Dog inherits all of Animal's fields and methods.
- **`super(name)`** — calls the parent's constructor. This must be the first line in the subclass constructor. The parent is responsible for initializing its own fields.
- **`@Override`** — tells the compiler this method is overriding a parent method. If you misspell the method name, the compiler will catch it. Optional but strongly recommended.
- **Private fields and getters** — Animal's `name` field is `private`, so Dog can't access it directly. Dog uses `getName()` instead. This is encapsulation in action across an inheritance hierarchy.

With inheritance, you can also store different subclasses in a collection of the parent type:

```java
ArrayList<Animal> animals = new ArrayList<>();
animals.add(new Dog("Buddy"));
animals.add(new Cat("Whiskers"));

for (Animal a : animals) {
    a.speak();  // Calls the right version for each type
}
```

This is **polymorphism** — one variable type (`Animal`), multiple behaviors depending on the actual object. Each subclass's `speak()` runs when called, even though the variable is declared as `Animal`.

## Destructors: Not Needed

C++ requires destructors to free memory manually. Java doesn't — the garbage collector handles all cleanup automatically. There is no `~ClassName()` equivalent.

If your class holds resources like file handles or database connections, use **try-with-resources** (see [09 - Unique Features](09-unique-features.md)) to ensure they're closed properly.

---

[← Previous: I/O Streams](07-io-streams.md) | [Next: Unique Features →](09-unique-features.md)
