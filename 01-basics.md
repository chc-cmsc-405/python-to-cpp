# 01 - Basics

[← Back to C++ Guide](README.md)

Every C++ program needs a `main()` function as its entry point—unlike Python where code runs from the top of the file. You'll also need to include header files for input/output functionality. The basic syntax will feel familiar, but pay attention to semicolons (required after every statement) and braces (used instead of indentation for code blocks).

---

## Comments

| Python | C++ |
|--------|-----|
| `# Single line comment` | `// Single line comment` |
| `""" Multi-line comment """` | `/* Multi-line comment */` |

## Hello World

**Python:**
```python
print("Hello, World!")
```

**C++:**
```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

## Output

| Python | C++ |
|--------|-----|
| `print(value)` | `std::cout << value << std::endl;` |
| `print(a, b, c)` | `std::cout << a << " " << b << " " << c << std::endl;` |
| `print(f"Value: {x}")` | `std::cout << "Value: " << x << std::endl;` |

## Input

| Python | C++ |
|--------|-----|
| `name = input("Enter name: ")` | `std::string name;`<br>`std::cout << "Enter name: ";`<br>`std::cin >> name;` |
| `num = int(input("Enter number: "))` | `int num;`<br>`std::cout << "Enter number: ";`<br>`std::cin >> num;` |

## Variables

**Python:**
```python
x = 10          # No type declaration
name = "Alice"  # Type inferred
pi = 3.14       # Type inferred
```

**C++:**
```cpp
int x = 10;                  // Type required
std::string name = "Alice";  // Type required
double pi = 3.14;            // Type required
auto y = 20;                 // Type inference with auto (C++11)
```

## Constants

| Python | C++ |
|--------|-----|
| `PI = 3.14159` (convention only) | `const double PI = 3.14159;` |
| No true constants | `constexpr int MAX = 100;` |

---

[Next: Data Types →](02-data-types.md)
