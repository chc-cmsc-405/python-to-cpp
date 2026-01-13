# 07 - Object-Oriented Programming

[← Back to C++ Guide](README.md)

C++ was one of the first languages to support object-oriented programming and takes it seriously. Classes have explicit access modifiers (`public`, `private`, `protected`) that the compiler enforces—not just naming conventions like Python's `_private`. Constructors use the class name instead of `__init__`, and there's no `self` parameter—member variables are accessed directly or through the `this` pointer.

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

**C++:**
```cpp
#include <string>
#include <iostream>

class Dog {
private:
    std::string name;
    int age;

public:
    // Constructor
    Dog(std::string n, int a) {
        name = n;
        age = a;
    }

    void bark() {
        std::cout << name << " says woof!" << std::endl;
    }

    int getAge() {
        return age;
    }
};
```

## Creating Objects

**Python:**
```python
my_dog = Dog("Buddy", 3)
my_dog.bark()
print(my_dog.get_age())
```

**C++:**
```cpp
Dog myDog("Buddy", 3);
myDog.bark();
std::cout << myDog.getAge() << std::endl;
```

## Key OOP Differences

| Concept | Python | C++ |
|---------|--------|-----|
| **Constructor** | `def __init__(self):` | `ClassName() { }` |
| **Self reference** | `self` (explicit parameter) | `this` (implicit pointer) |
| **Access modifiers** | Convention only (`_private`) | `public:`, `private:`, `protected:` |
| **Inheritance** | `class Child(Parent):` | `class Child : public Parent { }` |
| **Multiple inheritance** | Supported | Supported |

## Access Modifiers

Python uses naming conventions. C++ enforces access:

**Python:**
```python
class Person:
    def __init__(self, name):
        self.name = name       # Public (convention)
        self._age = 0          # "Private" (convention only)
        self.__secret = "x"    # Name-mangled
```

**C++:**
```cpp
class Person {
public:
    std::string name;      // Accessible from anywhere

private:
    int age;               // Only accessible within class

protected:
    std::string secret;    // Accessible in class and subclasses
};
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

**C++:**
```cpp
class Animal {
protected:
    std::string name;

public:
    Animal(std::string n) : name(n) {}

    virtual void speak() {
        // Base implementation
    }
};

class Dog : public Animal {
public:
    Dog(std::string n) : Animal(n) {}

    void speak() override {
        std::cout << name << " says woof!" << std::endl;
    }
};
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

**C++:**
```cpp
class Counter {
private:
    int count;

public:
    Counter() : count(0) {}

    Counter& increment() {
        this->count++;    // 'this' is a pointer
        return *this;     // Return reference for chaining
    }
};
```

---

[← Previous: Functions](06-functions.md) | [Next: Unique Features →](08-unique-features.md)
