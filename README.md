# C++ For Python Programmers

You already know Python. This guide helps you learn C++ by showing side-by-side comparisons with familiar Python syntax.

## How to Use This Guide

- **[Reading Guide](reading-guide.md)** — Phase-aligned reading assignments for CMSC-405
- **Quick Reference** — This README has dense comparison tables for quick lookup
- **Deep Dive** — Individual pages (linked below) cover specific topics in detail with code examples
- **Side-by-Side** — Python code on the left, C++ on the right

---

## About C++

C++ is a general-purpose programming language designed for systems programming and performance-critical applications. It compiles directly to machine code, giving programmers fine-grained control over memory and hardware. C++ is widely used in game engines, operating systems, browsers, and embedded systems. Below, you will find a simple guide for Python programmers as an introduction to C++. The syntax will feel familiar in many places—both languages share roots in C-style structure—but C++ requires more explicit type declarations and manual resource management.

---

## Key Differences

C++ is a statically-typed, compiled language. Unlike Python where you can just run your code, C++ requires a compilation step that checks for errors before execution. You must declare variable types, use braces for code blocks, and end statements with semicolons.

| Aspect | Python | C++ |
|--------|--------|-----|
| **Typing** | Dynamic | Static (declare types) |
| **Execution** | Interpreted | Compiled |
| **Memory** | Garbage collected | Manual (or RAII) |
| **Blocks** | Indentation | Braces `{ }` |
| **Semicolons** | Not required | Required |
| **Main function** | Optional | Required: `int main()` |

---

## Quick Reference

### Output & Input

C++ uses `std::cout` for output and `std::cin` for input. The `<<` operator sends data to the output stream, while `>>` reads from input. Unlike Python's `input()`, C++ separates the prompt from the actual input operation.

| Task | Python | C++ |
|------|--------|-----|
| Print | `print("hi")` | `std::cout << "hi" << std::endl;` |
| Print variable | `print(x)` | `std::cout << x << std::endl;` |
| Input string | `x = input()` | `std::cin >> x;` |
| Input with prompt | `x = input("Enter: ")` | `std::cout << "Enter: "; std::cin >> x;` |

### Variables & Constants

In C++, you must declare the type of every variable. The compiler uses this information to catch errors and optimize your code. Use `const` to create true constants that the compiler enforces.

| Task | Python | C++ |
|------|--------|-----|
| Integer | `x = 5` | `int x = 5;` |
| Float | `x = 3.14` | `double x = 3.14;` |
| String | `s = "hello"` | `std::string s = "hello";` |
| Boolean | `flag = True` | `bool flag = true;` |
| Constant | `PI = 3.14` | `const double PI = 3.14;` |

### Control Flow

Control structures work similarly, but C++ requires parentheses around conditions and braces around code blocks. Python's `elif` becomes `else if` in C++.

| Task | Python | C++ |
|------|--------|-----|
| If | `if x > 0:` | `if (x > 0) {` |
| Else if | `elif x < 0:` | `} else if (x < 0) {` |
| Else | `else:` | `} else {` |
| Ternary | `"yes" if x else "no"` | `x ? "yes" : "no"` |

### Loops

C++ uses the traditional three-part `for` loop with initialization, condition, and increment. The range-based `for` loop (C++11) is similar to Python's `for-each` pattern.

| Task | Python | C++ |
|------|--------|-----|
| For (range) | `for i in range(5):` | `for (int i = 0; i < 5; i++) {` |
| For (each) | `for x in items:` | `for (int x : items) {` |
| While | `while x > 0:` | `while (x > 0) {` |

### Functions

C++ functions require explicit return types and parameter types. If a function doesn't return anything, use `void`. Functions must be declared before they're called.

| Task | Python | C++ |
|------|--------|-----|
| Define | `def foo():` | `void foo() {` |
| With return | `def add(a, b): return a + b` | `int add(int a, int b) { return a + b; }` |
| Default param | `def greet(name="World"):` | `void greet(std::string name = "World") {` |

### Data Structures

C++ `vector` is the equivalent of Python's list—a resizable array. Unlike Python lists, vectors can only hold one type. Maps work like dictionaries but require type declarations for both keys and values.

| Task | Python | C++ |
|------|--------|-----|
| List / Vector | `[1, 2, 3]` | `std::vector<int> v = {1, 2, 3};` |
| Append | `list.append(x)` | `vec.push_back(x);` |
| Access | `list[0]` | `vec[0]` |
| Length | `len(list)` | `vec.size()` |
| Dictionary / Map | `{"a": 1}` | `std::map<std::string, int> m = {{"a", 1}};` |

### Classes

C++ classes explicitly separate public and private members. The constructor has the same name as the class (no `__init__`). There's no `self` parameter—member variables are accessed directly.

| Task | Python | C++ |
|------|--------|-----|
| Define | `class Dog:` | `class Dog { };` |
| Constructor | `def __init__(self):` | `Dog() { }` |
| Method | `def bark(self):` | `void bark() {` |
| Create object | `d = Dog()` | `Dog d;` |

### Operators & Comments

Most operators are similar, but watch out for division: in C++, dividing two integers gives an integer result. Use `pow()` for exponents instead of `**`. Logical operators use symbols instead of words.

| Task | Python | C++ |
|------|--------|-----|
| And / Or / Not | `and` `or` `not` | `&&` `\|\|` `!` |
| Exponent | `x ** 2` | `pow(x, 2)` |
| Integer division | `7 // 2` → `3` | `7 / 2` → `3` |
| Float division | `7 / 2` → `3.5` | `7.0 / 2` → `3.5` |
| Comment | `# comment` | `// comment` |
| Multi-line | `""" comment """` | `/* comment */` |

---

## Common Includes

C++ requires you to include libraries for most functionality. These are the headers you'll use most often:

```cpp
#include <iostream>   // cout, cin
#include <string>     // std::string
#include <vector>     // std::vector
#include <map>        // std::map
#include <cmath>      // pow, sqrt
```

---

## Detailed Sections

For more examples and in-depth explanations, see:

| Section | Topics |
|---------|--------|
| [01 - Basics](01-basics.md) | Comments, Hello World, I/O, variables, constants |
| [02 - Data Types](02-data-types.md) | Types, type conversion |
| [03 - Operators](03-operators.md) | Arithmetic, comparison, logical |
| [04 - Control Flow](04-control-flow.md) | If/else, for, while, break/continue |
| [05 - Data Structures](05-data-structures.md) | Vectors, maps, strings, file I/O |
| [06 - Functions](06-functions.md) | Definition, parameters, defaults, void |
| [07 - Custom Types](07-oop.md) | Structs, classes, constructors, inheritance |
| [08 - Unique Features](08-unique-features.md) | Pointers, references, arrow operator, memory, headers |

---

*This guide covers the basics. C++ has many more features that you'll learn throughout the course.*
