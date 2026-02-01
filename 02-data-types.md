# 02 - Data Types

[← Back to C++ Guide](README.md)

C++ is statically typed—every variable must have a declared type, and that type cannot change. This catches many errors at compile time rather than runtime. C++ also distinguishes between different sizes of numbers (`int`, `long`, `float`, `double`) and has a separate `char` type for single characters, unlike Python where `'a'` is just a one-character string.

---

## Primitive Types

| Concept | Python | C++ |
|---------|--------|-----|
| **Integer** | `x = 42` | `int x = 42;` |
| **Float** | `x = 3.14` | `double x = 3.14;` or `float x = 3.14f;` |
| **Boolean** | `True`, `False` | `true`, `false` |
| **Character** | `'a'` (just a string) | `'a'` (distinct `char` type) |
| **None/Null** | `None` | `nullptr` (for pointers) |

---

## Strings

In Python, strings are a built-in type with methods. In C++, you use `std::string` from the `<string>` header—it's a class with methods similar to Python's string methods.

### String Basics

| Concept | Python | C++ |
|---------|--------|-----|
| **Create** | `s = "hello"` | `std::string s = "hello";` |
| **Length** | `len(s)` | `s.length()` or `s.size()` |
| **Concatenate** | `s1 + s2` | `s1 + s2` |
| **Access char** | `s[0]` | `s[0]` |
| **Check empty** | `if not s:` | `if (s.empty())` |
| **Compare** | `s1 == s2` | `s1 == s2` or `s1.compare(s2)` |

**Python:**
```python
text = "Hello, World!"
print(len(text))        # 13
print(text[0])          # H
```

**C++:**
```cpp
#include <string>

std::string text = "Hello, World!";
std::cout << text.length() << std::endl;  // 13
std::cout << text[0] << std::endl;        // H
```

### String Operations (Finding & Extracting)

| Concept | Python | C++ |
|---------|--------|-----|
| **Find** | `s.find("ell")` | `s.find("ell")` |
| **Find from end** | `s.rfind("l")` | `s.rfind("l")` |
| **Substring** | `s[1:4]` | `s.substr(1, 3)` (start, length) |
| **Starts with** | `s.startswith("He")` | `s.find("He") == 0` |
| **Ends with** | `s.endswith("!")` | `s.rfind("!") == s.length()-1` |

```cpp
std::string text = "Hello, World!";
std::cout << text.find("World") << std::endl;    // 7
std::cout << text.rfind("o") << std::endl;       // 8 (last 'o')
std::cout << text.substr(0, 5) << std::endl;     // Hello
std::cout << text.substr(7) << std::endl;        // World! (to end)
```

**Note:** `find()` returns `std::string::npos` if not found (a large number, not -1 like Python).

### String Modifiers

| Concept | Python | C++ |
|---------|--------|-----|
| **Append** | `s += "more"` | `s += "more"` or `s.append("more")` |
| **Insert** | N/A (use slicing) | `s.insert(5, "text")` |
| **Erase** | N/A (use slicing) | `s.erase(5, 3)` (start, count) |
| **Replace** | `s.replace("old", "new")` | `s.replace(pos, len, "new")` |
| **Clear** | `s = ""` | `s.clear()` |

```cpp
std::string text = "Hello, World!";
text.append("!");                    // "Hello, World!!"
text.insert(7, "Beautiful ");        // "Hello, Beautiful World!!"
text.erase(7, 10);                   // "Hello, World!!"
text.replace(0, 5, "Hi");            // "Hi, World!!"
```

**Note:** C++ `replace()` works by position, not by searching. To replace all occurrences of a substring, you need a loop with `find()`.

---

## Character Functions

C++ provides character functions in `<cctype>`. In Python, these are methods on strings. In C++, they're standalone functions that take a character.

| Task | Python | C++ |
|------|--------|-----|
| **Is letter?** | `c.isalpha()` | `isalpha(c)` |
| **Is digit?** | `c.isdigit()` | `isdigit(c)` |
| **Is alphanumeric?** | `c.isalnum()` | `isalnum(c)` |
| **Is whitespace?** | `c.isspace()` | `isspace(c)` |
| **Is uppercase?** | `c.isupper()` | `isupper(c)` |
| **Is lowercase?** | `c.islower()` | `islower(c)` |
| **To uppercase** | `c.upper()` | `toupper(c)` |
| **To lowercase** | `c.lower()` | `tolower(c)` |

**Python:**
```python
text = "Hello123"
for c in text:
    if c.isalpha():
        print(c.upper())
    elif c.isdigit():
        print(c)
```

**C++:**
```cpp
#include <cctype>
#include <string>

std::string text = "Hello123";
for (char c : text) {
    if (isalpha(c)) {
        std::cout << (char)toupper(c);
    } else if (isdigit(c)) {
        std::cout << c;
    }
}
```

**Note:** `toupper()` and `tolower()` return an `int`, so cast to `char` when outputting.

---

## Type Conversions

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

### All Conversion Functions

| Function | Converts |
|----------|----------|
| `std::stoi(s)` | string → int |
| `std::stol(s)` | string → long |
| `std::stoll(s)` | string → long long |
| `std::stof(s)` | string → float |
| `std::stod(s)` | string → double |
| `std::to_string(n)` | any number → string |

---

[← Previous: Basics](01-basics.md) | [Next: Operators →](03-operators.md)
