# 02 - Data Types

[← Back to C++ Guide](README.md)

C++ is statically typed—every variable must have a declared type, and that type cannot change. This catches many errors at compile time rather than runtime. C++ also distinguishes between different sizes of numbers (`int`, `long`, `float`, `double`) and has a separate `char` type for single characters, unlike Python where `'a'` is just a one-character string.

---

## Basic Types

| Concept | Python | C++ |
|---------|--------|-----|
| **Integer** | `x = 42` | `int x = 42;` |
| **Float** | `x = 3.14` | `double x = 3.14;` or `float x = 3.14f;` |
| **Boolean** | `True`, `False` | `true`, `false` |
| **String** | `"hello"` or `'hello'` | `"hello"` (use `std::string` for operations) |
| **Character** | `'a'` (just a string) | `'a'` (distinct `char` type) |
| **None/Null** | `None` | `nullptr` (for pointers) |

## Strings

In Python, strings are a built-in type. In C++, you need to include the string library:

```cpp
#include <string>

std::string name = "Alice";
```

## Type Conversion

| Python | C++ |
|--------|-----|
| `int("42")` | `std::stoi("42")` |
| `float("3.14")` | `std::stod("3.14")` |
| `str(42)` | `std::to_string(42)` |
| `int(3.7)` → `3` | `(int)3.7` or `static_cast<int>(3.7)` |

**Python:**
```python
num_str = "42"
num = int(num_str)      # String to int
pi = float("3.14")      # String to float
text = str(100)         # Int to string
```

**C++:**
```cpp
#include <string>

std::string num_str = "42";
int num = std::stoi(num_str);       // String to int
double pi = std::stod("3.14");      // String to double
std::string text = std::to_string(100);  // Int to string
```

---

[← Previous: Basics](01-basics.md) | [Next: Operators →](03-operators.md)
