# 08 - Custom Types: Structs and Classes

[← Back to C++ Guide](README.md)

C++ provides two ways to define custom types: **structs** and **classes**. Structs are simpler—great for grouping related data together. Classes add encapsulation with access modifiers (`public`, `private`). In C++, structs and classes are almost identical; the only difference is that struct members are public by default, while class members are private by default.

---

## Structs

Structs group related data together. Python doesn't have a direct equivalent, but dataclasses or namedtuples are similar.

### Defining a Struct

**Python (using dataclass):**
```python
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float

p = Point(3.0, 4.0)
print(p.x, p.y)
```

**C++:**
```cpp
struct Point {
    double x;
    double y;
};

int main() {
    Point p = {3.0, 4.0};  // Brace initialization
    std::cout << p.x << ", " << p.y << std::endl;
    return 0;
}
```

### Struct with Multiple Fields

**Python:**
```python
@dataclass
class Student:
    name: str
    id: int
    gpa: float
```

**C++:**
```cpp
struct Student {
    std::string name;
    int id;
    double gpa;
};

// Creating a student
Student s = {"Alice", 12345, 3.8};
Student s2 = {"Bob", 67890, 3.5};
```

### Accessing and Modifying Members

**Python:**
```python
s = Student("Alice", 12345, 3.8)
print(s.name)      # Access
s.gpa = 3.9        # Modify
```

**C++:**
```cpp
Student s = {"Alice", 12345, 3.8};
std::cout << s.name << std::endl;  // Access
s.gpa = 3.9;                       // Modify
```

### Passing Structs to Functions

**C++:**
```cpp
// Pass by value (copy)
void printStudent(Student s) {
    std::cout << s.name << ": " << s.gpa << std::endl;
}

// Pass by const reference (read-only, no copy)
void displayStudent(const Student& s) {
    std::cout << s.name << ": " << s.gpa << std::endl;
}

// Pass by reference (can modify)
void updateGPA(Student& s, double newGPA) {
    s.gpa = newGPA;
}
```

**When to use which:**
- `Student s` — Makes a copy (safe but slower for large structs)
- `const Student& s` — Read-only access, no copy (fast and safe)
- `Student& s` — Can modify the original (use when you need to change it)

### Vectors of Structs

**Python:**
```python
students = [
    Student("Alice", 1, 3.8),
    Student("Bob", 2, 3.5),
    Student("Carol", 3, 3.9)
]

for s in students:
    print(s.name)
```

**C++:**
```cpp
std::vector<Student> students = {
    {"Alice", 1, 3.8},
    {"Bob", 2, 3.5},
    {"Carol", 3, 3.9}
};

for (const Student& s : students) {
    std::cout << s.name << std::endl;
}
```

### Structs vs Classes

| Aspect | Struct | Class |
|--------|--------|-------|
| **Default access** | Public | Private |
| **Typical use** | Simple data grouping | Data + behavior with encapsulation |
| **Convention** | Plain data, no/few methods | Methods, private data, constructors |

In C++, structs can have methods and constructors just like classes. The convention is to use structs for simple data and classes when you need encapsulation.

---

## Classes

Classes add encapsulation—the ability to hide data and control access through methods. C++ was one of the first languages to support object-oriented programming and takes it seriously. Classes have explicit access modifiers (`public`, `private`, `protected`) that the compiler enforces—not just naming conventions like Python's `_private`. Constructors use the class name instead of `__init__`, and there's no `self` parameter—member variables are accessed directly or through the `this` pointer.

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

[← Previous: I/O Streams](07-io-streams.md) | [Next: Unique Features →](09-unique-features.md)
