# 06 - Data Structures

[← Back to C++ Guide](README.md)

C++ provides several container types through its Standard Template Library (STL). The `vector` is most similar to Python's list—it's a resizable array that grows automatically. Unlike Python lists, C++ vectors can only hold one type (e.g., `vector<int>` holds only integers). Maps work like Python dictionaries but also require type declarations for both keys and values.

---

## Arrays

### C-Style Arrays

C-style arrays are fixed-size collections with no methods—just raw memory with index access.

```cpp
int numbers[5] = {1, 2, 3, 4, 5};  // Fixed size of 5
numbers[0] = 10;                    // Access by index
// numbers.size()  — Error! Arrays have no methods
// numbers.push_back(6)  — Error! Can't resize arrays
```

**Key limitations:**
- Size is fixed at compile time—can't grow or shrink
- No `.size()` method—you must track length separately
- When passing to functions, you must also pass the size

```cpp
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << std::endl;
    }
}
```

### STL Arrays (`std::array`)

`std::array` is a modern C++ wrapper around fixed-size arrays. It has the same performance as C arrays but includes helpful methods.

```cpp
#include <array>

std::array<int, 5> numbers = {1, 2, 3, 4, 5};  // Fixed size of 5
numbers[0] = 10;                    // Access by index
std::cout << numbers.size();        // 5 — has .size()!
std::cout << numbers.at(2);         // 3 — bounds-checked access
std::cout << numbers.front();       // 10 — first element
std::cout << numbers.back();        // 5 — last element
```

| Feature | C Array | `std::array` | `std::vector` |
|---------|---------|--------------|---------------|
| Fixed size | Yes | Yes | No (resizable) |
| Has `.size()` | No | Yes | Yes |
| Has `.at()` | No | Yes | Yes |
| Bounds checking | No | Yes (with `.at()`) | Yes (with `.at()`) |

**When to use:**
- **C arrays:** Low-level code, interfacing with C libraries
- **`std::array`:** Fixed-size collections where you want STL conveniences
- **`std::vector`:** When size may change, or you don't know size at compile time

## Lists

`std::list` is a doubly-linked list. It's efficient for inserting/removing elements anywhere, but has no random access.

```cpp
#include <list>

std::list<int> numbers = {1, 2, 3, 4, 5};
numbers.push_back(6);       // Add to end
numbers.push_front(0);      // Add to beginning
numbers.pop_back();         // Remove from end
numbers.pop_front();        // Remove from beginning
// numbers[2]  — Error! No random access with lists
```

| Feature | `std::list` | `std::vector` |
|---------|-------------|---------------|
| Random access `[i]` | No | Yes |
| `push_front` | Yes | No |
| Insert in middle | Fast | Slow |
| Memory | More overhead | Contiguous |

**When to use:** Lists are best when you frequently insert/remove from the middle. For most cases, prefer vectors.

## Vectors

`std::vector` is the closest equivalent to Python lists—a resizable array that grows automatically.

| Concept | Python | C++ |
|---------|--------|-----|
| **Create** | `my_list = [1, 2, 3]` | `std::vector<int> vec = {1, 2, 3};` |
| **Access** | `my_list[0]` | `vec[0]` or `vec.at(0)` |
| **Length** | `len(my_list)` | `vec.size()` |
| **Append** | `my_list.append(4)` | `vec.push_back(4);` |
| **Insert** | `my_list.insert(1, "x")` | `vec.insert(vec.begin() + 1, x);` |
| **Remove last** | `my_list.pop()` | `vec.pop_back();` |
| **Check empty** | `if not my_list:` | `if (vec.empty())` |

**Python:**
```python
numbers = [1, 2, 3, 4, 5]
numbers.append(6)
print(numbers[0])     # 1
print(len(numbers))   # 6
```

**C++:**
```cpp
#include <vector>

std::vector<int> numbers = {1, 2, 3, 4, 5};
numbers.push_back(6);
std::cout << numbers[0] << std::endl;      // 1
std::cout << numbers.size() << std::endl;  // 6
```

**When to use:** Vectors are the go-to choice for most situations. Use them unless you have a specific reason not to.

## Iterating Over Vectors

**Python:**
```python
for num in numbers:
    print(num)

for i, num in enumerate(numbers):
    print(f"{i}: {num}")
```

**C++:**
```cpp
// Range-based for loop
for (int num : numbers) {
    std::cout << num << std::endl;
}

// With index
for (int i = 0; i < numbers.size(); i++) {
    std::cout << i << ": " << numbers[i] << std::endl;
}
```

## Dictionaries / Maps

| Concept | Python | C++ |
|---------|--------|-----|
| **Create** | `d = {"a": 1, "b": 2}` | `std::map<std::string, int> m = {{"a", 1}, {"b", 2}};` |
| **Access** | `d["a"]` | `m["a"]` |
| **Check key** | `"a" in d` | `m.find("a") != m.end()` or `m.count("a") > 0` |
| **Add/Update** | `d["c"] = 3` | `m["c"] = 3;` |
| **Delete** | `del d["a"]` | `m.erase("a");` |

**Python:**
```python
scores = {"Alice": 95, "Bob": 87}
scores["Charlie"] = 92

if "Alice" in scores:
    print(scores["Alice"])
```

**C++:**
```cpp
#include <map>
#include <string>

std::map<std::string, int> scores = {{"Alice", 95}, {"Bob", 87}};
scores["Charlie"] = 92;

if (scores.count("Alice") > 0) {
    std::cout << scores["Alice"] << std::endl;
}
```

## Strings

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

[← Previous: Functions](05-functions.md) | [Next: I/O Streams →](07-io-streams.md)
