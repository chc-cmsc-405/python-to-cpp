# 05 - Data Structures

[← Back to C++ Guide](README.md)

C++ provides several container types through its Standard Template Library (STL). The `vector` is most similar to Python's list—it's a resizable array that grows automatically. Unlike Python lists, C++ vectors can only hold one type (e.g., `vector<int>` holds only integers). Maps work like Python dictionaries but also require type declarations for both keys and values.

---

## Arrays / Lists / Vectors

Python uses lists. C++ has arrays and vectors. **Vectors** are the closest equivalent to Python lists.

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

| Concept | Python | C++ |
|---------|--------|-----|
| **Create** | `s = "hello"` | `std::string s = "hello";` |
| **Length** | `len(s)` | `s.length()` or `s.size()` |
| **Concatenate** | `s1 + s2` | `s1 + s2` |
| **Find** | `s.find("ell")` | `s.find("ell")` |
| **Substring** | `s[1:4]` | `s.substr(1, 3)` (start, length) |
| **Access char** | `s[0]` | `s[0]` |

**Python:**
```python
text = "Hello, World!"
print(len(text))        # 13
print(text[0:5])        # Hello
print(text.find("World"))  # 7
```

**C++:**
```cpp
#include <string>

std::string text = "Hello, World!";
std::cout << text.length() << std::endl;     // 13
std::cout << text.substr(0, 5) << std::endl; // Hello
std::cout << text.find("World") << std::endl; // 7
```

---

## File I/O

Python's file handling is simpler, but C++ gives you more control. Use `ifstream` for reading and `ofstream` for writing.

### Reading a File

**Python:**
```python
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

**C++:**
```cpp
#include <fstream>
#include <string>

std::ifstream file("data.txt");
std::string line;
while (std::getline(file, line)) {
    std::cout << line << std::endl;
}
file.close();
```

### Writing to a File

**Python:**
```python
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
```

**C++:**
```cpp
#include <fstream>

std::ofstream file("output.txt");
file << "Hello, World!" << std::endl;
file.close();
```

### Common File Operations

| Task | Python | C++ |
|------|--------|-----|
| **Open for reading** | `open("f.txt", "r")` | `std::ifstream file("f.txt");` |
| **Open for writing** | `open("f.txt", "w")` | `std::ofstream file("f.txt");` |
| **Read line** | `line = file.readline()` | `std::getline(file, line);` |
| **Read all lines** | `for line in file:` | `while (std::getline(file, line))` |
| **Write line** | `file.write(text)` | `file << text << std::endl;` |
| **Check if open** | N/A (raises exception) | `if (file.is_open())` |
| **Close file** | `file.close()` | `file.close();` |

### Reading CSV Data

**Python:**
```python
with open("data.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name = parts[0]
        score = int(parts[1])
```

**C++:**
```cpp
#include <fstream>
#include <sstream>
#include <string>

std::ifstream file("data.csv");
std::string line;

while (std::getline(file, line)) {
    std::stringstream ss(line);
    std::string name;
    std::string scoreStr;

    std::getline(ss, name, ',');
    std::getline(ss, scoreStr, ',');
    int score = std::stoi(scoreStr);
}
file.close();
```

### Checking for Errors

**C++:**
```cpp
std::ifstream file("data.txt");

if (!file.is_open()) {
    std::cout << "Error: Could not open file" << std::endl;
    return 1;
}

// File operations here...

file.close();
```

---

[← Previous: Control Flow](04-control-flow.md) | [Next: Functions →](06-functions.md)
