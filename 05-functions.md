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

In Python, the behavior depends on the type:
- **Immutable types** (`int`, `str`, `tuple`): Changes inside a function don't affect the original—similar to pass by value
- **Mutable types** (`list`, `dict`): Changes inside a function affect the original—similar to pass by reference

In C++, you choose explicitly with the `&` symbol, regardless of type:

**C++:**
```cpp
#include <iostream>

// Pass by value (copy) — changes stay inside the function
void doubleByValue(int x) {
    x = x * 2;
    std::cout << "Inside function: " << x << std::endl;
}

// Pass by reference (modify original) — changes affect the caller
void doubleByReference(int& x) {
    x = x * 2;
    std::cout << "Inside function: " << x << std::endl;
}

int main() {
    int a = 5;
    doubleByValue(a);
    std::cout << "After doubleByValue: " << a << std::endl;  // Still 5!

    int b = 5;
    doubleByReference(b);
    std::cout << "After doubleByReference: " << b << std::endl;  // Now 10
    return 0;
}
```

**Output:**
```
Inside function: 10
After doubleByValue: 5
Inside function: 10
After doubleByReference: 10
```

The `&` in the parameter makes all the difference—without it, the function works on a copy.

## Const References

When you pass by reference but don't need to modify the data, use `const`.

**Note:** `const` is unique to C++ (and C). Python has no equivalent—you can't tell Python "don't let this function modify my list." In C++, the compiler enforces `const` at compile time, catching accidental modifications before your code even runs.

```cpp
// Pass by const reference (read-only, no copy)
void printScores(const std::vector<int>& scores) {
    for (int s : scores) {
        std::cout << s << std::endl;
    }
    // scores.push_back(100);  // Error! Can't modify const reference
}

// Pass by reference (can modify)
void addScore(std::vector<int>& scores, int newScore) {
    scores.push_back(newScore);  // OK - modifies original vector
}
```

**Why use `const&`?**
- **Efficiency** — Avoids copying large data (vectors, strings)
- **Safety** — Compiler prevents accidental modification
- **Intent** — Makes it clear the function only reads the data

| Parameter Type | Copies Data? | Can Modify? | Use When |
|----------------|--------------|-------------|----------|
| `int x` | Yes | No (copy) | Small types (int, double, char) |
| `vector<int>& v` | No | Yes | Need to modify the original |
| `const vector<int>& v` | No | No | Read-only access to large data |

**Rule of thumb:** For vectors and strings, prefer `const T&` unless you need to modify.

---

[← Previous: Control Flow](04-control-flow.md) | [Next: Data Structures →](06-data-structures.md)
