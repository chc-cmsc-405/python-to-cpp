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

## Console Output

C++ uses `std::cout` (character output) to print to the console. The `<<` operator sends data to the output stream.

| Python | C++ |
|--------|-----|
| `print(value)` | `std::cout << value << std::endl;` |
| `print(a, b, c)` | `std::cout << a << " " << b << " " << c << std::endl;` |
| `print(f"Value: {x}")` | `std::cout << "Value: " << x << std::endl;` |

## Console Input

C++ uses `std::cin` (character input) to read from the keyboard. The `>>` operator reads data from the input stream.

| Python | C++ |
|--------|-----|
| `name = input("Enter name: ")` | `std::string name;`<br>`std::cout << "Enter name: ";`<br>`std::cin >> name;` |
| `num = int(input("Enter number: "))` | `int num;`<br>`std::cout << "Enter number: ";`<br>`std::cin >> num;` |

**Note:** `cin >>` stops at whitespace. To read a full line (including spaces), use `getline()` — see [06 - I/O Streams](06-io-streams.md).

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

## Header Files and #include

C++ separates declarations (`.h` files) from implementations (`.cpp` files).

```cpp
// Standard library headers (no .h)
#include <iostream>  // Input/output
#include <string>    // String class
#include <vector>    // Vector class
#include <map>       // Map class
#include <cmath>     // Math functions

// Your own headers (with .h)
#include "myfile.h"
```

**Why?**
- Allows separate compilation
- Reduces compile time for large projects
- Enables code organization

## Namespaces

C++ uses namespaces to avoid naming conflicts:

```cpp
// Using the std namespace explicitly
std::cout << "Hello" << std::endl;
std::string name = "Alice";
std::vector<int> nums;

// Or import the namespace (less recommended)
using namespace std;
cout << "Hello" << endl;
```

## Compilation Process

Unlike Python's immediate execution, C++ requires compilation:

```bash
# Compile source to executable
g++ -o myprogram myprogram.cpp

# Run the executable
./myprogram
```

**Multi-file compilation:**
```bash
# Compile multiple files
g++ -o myprogram main.cpp helper.cpp

# Or compile separately and link
g++ -c main.cpp       # Creates main.o
g++ -c helper.cpp     # Creates helper.o
g++ -o myprogram main.o helper.o  # Link
```

---

[Next: Data Types →](02-data-types.md)
