# 07 - I/O Streams

[← Back to C++ Guide](README.md)

C++ uses a unified "streams" model for input and output. Whether you're reading from the keyboard, a file, or a string, you use the same operators (`<<`, `>>`) and functions (`getline`). Once you understand streams, you can work with any input source using the same patterns.

---

## The Streams Concept

| Stream | Type | Purpose |
|--------|------|---------|
| `cin` | `istream` | Read from keyboard (console input) |
| `cout` | `ostream` | Write to screen (console output) |
| `ifstream` | Input file stream | Read from a file |
| `ofstream` | Output file stream | Write to a file |
| `stringstream` | String stream | Read from / write to a string |

**Key insight:** `getline()` and `>>` work the same way on ALL input streams.

```cpp
std::string line;
std::getline(std::cin, line);   // Read line from keyboard
std::getline(file, line);       // Read line from file — same syntax!
std::getline(ss, line);         // Read line from stringstream — same syntax!
```

---

## Reading Lines with getline()

The `>>` operator stops at whitespace. Use `getline()` to read an entire line including spaces.

**Python:**
```python
name = input("Enter your full name: ")  # Reads entire line
```

**C++:**
```cpp
std::string name;
std::cout << "Enter your full name: ";
std::getline(std::cin, name);  // Reads entire line including spaces
```

### getline vs >> Comparison

| Input | `cin >> name` | `getline(cin, name)` |
|-------|---------------|----------------------|
| `Alice` | `Alice` | `Alice` |
| `Alice Smith` | `Alice` (stops at space) | `Alice Smith` (full line) |

**Rule of thumb:** Use `getline()` when input might contain spaces.

---

## File I/O

Use `ifstream` to read from files and `ofstream` to write to files. Include the `<fstream>` header.

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

### Checking for Errors

Always check if the file opened successfully:

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

## String Streams

`stringstream` lets you parse a string as if it were an input stream. This is useful for splitting strings or parsing CSV data.

Include the `<sstream>` header.

### Parsing CSV Data

**Sample file (`grades.csv`):**
```
Alice,Math,95
Bob,English,87
Charlie,Math,92
```

**Python:**
```python
with open("grades.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        name = parts[0]
        subject = parts[1]
        score = int(parts[2])
```

**C++:**
```cpp
#include <fstream>
#include <sstream>
#include <string>

std::ifstream file("grades.csv");
std::string line;

while (std::getline(file, line)) {
    std::stringstream ss(line);
    std::string name;
    std::string subject;
    std::string scoreStr;

    std::getline(ss, name, ',');       // Read until first comma
    std::getline(ss, subject, ',');    // Read until second comma
    std::getline(ss, scoreStr);        // Read rest of line
    int score = std::stoi(scoreStr);
}

file.close();
```

Python's `split(",")` returns all parts at once. In C++, you call `getline()` once per field, reading until each delimiter.

### getline with Delimiter

`getline()` can use a custom delimiter (not just newline):

```cpp
std::stringstream ss("apple,banana,cherry");
std::string fruit;

while (std::getline(ss, fruit, ',')) {
    std::cout << fruit << std::endl;
}
// Output: apple, banana, cherry (each on own line)
```

---

## Common Patterns

### Load Data into a Vector

```cpp
#include <fstream>
#include <vector>
#include <string>

std::vector<std::string> loadLines(const std::string& filename) {
    std::vector<std::string> lines;
    std::ifstream file(filename);
    std::string line;

    while (std::getline(file, line)) {
        lines.push_back(line);
    }

    file.close();
    return lines;
}
```

### Load Numbers from a File

```cpp
std::vector<double> loadNumbers(const std::string& filename) {
    std::vector<double> numbers;
    std::ifstream file(filename);
    double value;

    while (file >> value) {
        numbers.push_back(value);
    }

    file.close();
    return numbers;
}
```

---

## Summary

| Task | Code |
|------|------|
| Read line from keyboard | `std::getline(std::cin, line);` |
| Read line from file | `std::getline(file, line);` |
| Read until delimiter | `std::getline(ss, token, ',');` |
| Open file for reading | `std::ifstream file("name.txt");` |
| Open file for writing | `std::ofstream file("name.txt");` |
| Check if file opened | `if (!file.is_open()) { ... }` |
| Convert string to int | `std::stoi(str)` |
| Convert string to double | `std::stod(str)` |

---

[← Previous: Data Structures](06-data-structures.md) | [Next: Custom Types →](08-custom-types.md)
