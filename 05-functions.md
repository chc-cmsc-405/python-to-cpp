# 05 - Functions

[← Back to C++ Guide](README.md)

C++ functions require you to declare the return type and the type of each parameter. Use `void` if the function doesn't return anything. Unlike Python, functions must be declared or defined before they're called—the compiler reads top-to-bottom. C++ also lets you choose whether to pass arguments by value (copy) or by reference (modify the original).

---

## Basic Function

**Python:**
```python
def greet(name):
    return f"Hello, {name}!"

message = greet("Alice")
```

**C++:**
```cpp
#include <string>

std::string greet(std::string name) {
    return "Hello, " + name + "!";
}

int main() {
    std::string message = greet("Alice");
    return 0;
}
```

**Key difference:** In C++, you must declare the return type and parameter types.

## Function with Multiple Parameters

**Python:**
```python
def add(a, b):
    return a + b
```

**C++:**
```cpp
int add(int a, int b) {
    return a + b;
}
```

## Default Parameters

**Python:**
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Alice")           # "Hello, Alice!"
greet("Alice", "Hi")     # "Hi, Alice!"
```

**C++:**
```cpp
std::string greet(std::string name, std::string greeting = "Hello") {
    return greeting + ", " + name + "!";
}

greet("Alice");          // "Hello, Alice!"
greet("Alice", "Hi");    // "Hi, Alice!"
```

## Void Functions (No Return Value)

**Python:**
```python
def say_hello():
    print("Hello!")
    # No return statement needed
```

**C++:**
```cpp
void say_hello() {
    std::cout << "Hello!" << std::endl;
    // No return statement needed
}
```

## Function Declaration Order

In C++, functions must be declared before they're used:

```cpp
// Option 1: Define before main
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3);
    return 0;
}

// Option 2: Forward declaration
int add(int a, int b);  // Declaration

int main() {
    int result = add(5, 3);
    return 0;
}

int add(int a, int b) {  // Definition
    return a + b;
}
```

## Pass by Value vs Reference

In Python, mutable objects (lists, dicts) are passed by reference. In C++, you must be explicit:

**C++:**
```cpp
// Pass by value (copy)
void doubleValue(int x) {
    x = x * 2;  // Only changes local copy
}

// Pass by reference (modify original)
void doubleValue(int& x) {
    x = x * 2;  // Changes original variable
}

int main() {
    int num = 5;
    doubleValue(num);  // Depends on which version is called
    return 0;
}
```

---

[← Previous: Control Flow](04-control-flow.md) | [Next: Data Structures →](06-data-structures.md)
