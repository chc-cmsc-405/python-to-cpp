# 09 - C++ Unique Features

[← Back to C++ Guide](README.md)

These concepts don't have direct Python equivalents. Pointers and references give you direct access to memory addresses—powerful but requiring careful handling. Manual memory management means you're responsible for allocating and freeing memory (though modern C++ offers smart pointers to help). Header files separate declarations from implementations, enabling faster compilation of large projects.

---

## Pointers

Pointers store memory addresses. Python doesn't expose memory addresses directly.

```cpp
int x = 10;
int* ptr = &x;      // ptr holds the address of x
std::cout << ptr;   // Prints memory address
std::cout << *ptr;  // Dereference: prints 10
*ptr = 20;          // Changes x to 20
```

**Common pointer operations:**

| Operation | Syntax | Meaning |
|-----------|--------|---------|
| Declare pointer | `int* ptr;` | Pointer to an int |
| Get address | `&x` | Address of x |
| Dereference | `*ptr` | Value at address |
| Null pointer | `nullptr` | Points to nothing |

## References

References are aliases for existing variables. Once set, they can't be changed to reference something else.

```cpp
int x = 10;
int& ref = x;  // ref is an alias for x
ref = 20;      // Changes x to 20

std::cout << x;    // Prints 20
std::cout << ref;  // Prints 20 (same variable)
```

## Pointers vs References

| Aspect | Pointer | Reference |
|--------|---------|-----------|
| Can be null | Yes (`nullptr`) | No |
| Can be reassigned | Yes | No |
| Syntax to access | `*ptr` | `ref` (direct) |
| Must be initialized | No | Yes |

**When to use which:**
- **References:** Function parameters when you want to modify the original
- **Pointers:** When you need null, dynamic allocation, or reassignment

## Arrow Operator (->)

When you have a pointer to a struct or class, use the arrow operator `->` to access members. It's shorthand for dereferencing then accessing.

```cpp
struct Student {
    std::string name;
    double gpa;
};

Student s = {"Alice", 3.8};
Student* ptr = &s;

// These are equivalent:
std::cout << (*ptr).name << std::endl;  // Dereference, then access
std::cout << ptr->name << std::endl;    // Arrow operator (cleaner)

// Modifying through pointer
ptr->gpa = 3.9;
```

**Common pattern with dynamic allocation:**
```cpp
Student* s = new Student{"Bob", 3.5};
std::cout << s->name << std::endl;  // Use -> with pointers
std::cout << s->gpa << std::endl;
delete s;
```

| Syntax | Use When |
|--------|----------|
| `obj.member` | You have the object directly |
| `ptr->member` | You have a pointer to the object |

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

## Memory Management: Python vs C++

This is one of the biggest differences between Python and C++.

| Aspect | Python | C++ |
|--------|--------|-----|
| **Who manages memory** | Python (automatic) | You (manual) |
| **Allocation** | Automatic when you create objects | Explicit with `new` or stack |
| **Deallocation** | Garbage collector handles it | You must call `delete` |
| **Memory leaks** | Rare (GC cleans up) | Common if you forget `delete` |
| **Performance** | GC pauses can occur | Predictable, no GC pauses |
| **Control** | None | Complete |

### How Python Works (Garbage Collection)

In Python, you never think about memory:

```python
def process_data():
    data = [1, 2, 3, 4, 5]  # Memory allocated automatically
    result = sum(data)
    return result
    # When function ends, 'data' is cleaned up automatically by GC
```

Python uses **reference counting** plus a **garbage collector** to find and free unused memory. You just create objects and forget about them.

### How C++ Works (Manual Management)

In C++, you're responsible for memory you allocate on the heap:

```cpp
void process_data() {
    // Stack allocation - automatic cleanup when function ends
    int x = 10;
    std::vector<int> vec = {1, 2, 3};  // Cleaned up automatically

    // Heap allocation - YOU must clean up
    int* data = new int[100];
    // ... use data ...
    delete[] data;  // If you forget this = memory leak!
}
```

### Stack vs Heap

| Location | Lifetime | Speed | Size Limit | Cleanup |
|----------|----------|-------|------------|---------|
| **Stack** | Until scope ends | Fast | Limited (~1MB) | Automatic |
| **Heap** | Until you `delete` | Slower | Large (GBs) | Manual |

```cpp
// Stack (automatic cleanup)
int x = 10;
std::vector<int> vec = {1,2,3};

// Heap (manual cleanup required)
int* ptr = new int(42);        // Allocate
delete ptr;                    // Must deallocate!

int* arr = new int[10];        // Allocate array
delete[] arr;                  // Must use delete[] for arrays
```

### What Can Go Wrong

| Problem | What Happens | Python Equivalent |
|---------|--------------|-------------------|
| **Memory leak** | Forgot to `delete` — memory never freed | N/A (GC handles it) |
| **Use after free** | Access memory after `delete` — crash or garbage data | N/A |
| **Double delete** | Call `delete` twice — crash | N/A |
| **Dangling pointer** | Pointer to freed memory | N/A |

### Modern C++ (Smart Pointers)

Modern C++ provides smart pointers that work more like Python—automatic cleanup:

```cpp
#include <memory>

// unique_ptr: Automatically deleted when out of scope
std::unique_ptr<int> ptr = std::make_unique<int>(42);
// No delete needed! Cleaned up automatically like Python.

// shared_ptr: Reference counted (like Python objects)
std::shared_ptr<Dog> dog1 = std::make_shared<Dog>("Buddy");
std::shared_ptr<Dog> dog2 = dog1;  // Both point to same Dog
// Deleted automatically when last reference goes away
```

**Recommendation:** Use smart pointers in modern C++ whenever possible. They give you Python-like convenience with C++ performance.

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

## The `const` Keyword

C++ uses `const` extensively for safety:

```cpp
const int MAX = 100;           // Constant variable
const std::string& getName();  // Returns const reference
void print(const std::string& s);  // Won't modify s

// Const member function (doesn't modify object)
class Dog {
public:
    std::string getName() const {
        return name;
    }
};
```

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

---

[← Previous: Custom Types](08-custom-types.md) | [Back to C++ Guide](README.md)
