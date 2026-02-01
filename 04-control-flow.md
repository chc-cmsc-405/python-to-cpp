# 04 - Control Flow

[← Back to C++ Guide](README.md)

Control structures in C++ follow the same logic as Python but with different syntax. Conditions must be wrapped in parentheses, and code blocks use braces instead of indentation. Python's `elif` becomes `else if`. C++ also has a `do-while` loop that Python lacks—it guarantees at least one iteration before checking the condition.

---

## If / Else

**Python:**
```python
if x > 0:
    print("Positive")
elif x < 0:
    print("Negative")
else:
    print("Zero")
```

**C++:**
```cpp
if (x > 0) {
    std::cout << "Positive" << std::endl;
} else if (x < 0) {
    std::cout << "Negative" << std::endl;
} else {
    std::cout << "Zero" << std::endl;
}
```

**Key differences:**
- C++ requires parentheses `()` around the condition
- C++ uses braces `{}` instead of indentation
- `elif` becomes `else if`

## Ternary Operator

| Python | C++ |
|--------|-----|
| `result = "yes" if x > 0 else "no"` | `result = (x > 0) ? "yes" : "no";` |

## Switch Statement

C++ has `switch` for comparing one value against multiple options. Python traditionally uses if/elif chains (though Python 3.10 added `match-case`).

**Python (if/elif):**
```python
day = 3
if day == 1:
    print("Monday")
elif day == 2:
    print("Tuesday")
elif day == 3:
    print("Wednesday")
else:
    print("Other day")
```

**C++:**
```cpp
int day = 3;
switch (day) {
    case 1:
        std::cout << "Monday" << std::endl;
        break;
    case 2:
        std::cout << "Tuesday" << std::endl;
        break;
    case 3:
        std::cout << "Wednesday" << std::endl;
        break;
    default:
        std::cout << "Other day" << std::endl;
}
```

**Key points:**
- Each `case` must end with `break` or execution "falls through" to the next case
- `default` handles values that don't match any case (like `else`)
- `switch` only works with integers and characters, not strings

## For Loop

**Python:**
```python
# Range-based
for i in range(5):
    print(i)

# With start and end
for i in range(1, 10):
    print(i)

# Iterating over list
for item in my_list:
    print(item)
```

**C++:**
```cpp
// Traditional for loop
for (int i = 0; i < 5; i++) {
    std::cout << i << std::endl;
}

// With start and end
for (int i = 1; i < 10; i++) {
    std::cout << i << std::endl;
}

// Range-based for loop (C++11)
for (int item : my_vector) {
    std::cout << item << std::endl;
}
```

## While Loop

**Python:**
```python
while x > 0:
    print(x)
    x -= 1
```

**C++:**
```cpp
while (x > 0) {
    std::cout << x << std::endl;
    x--;
}
```

## Do-While Loop

C++ has a do-while loop that Python doesn't have:

```cpp
// Executes at least once
do {
    std::cout << x << std::endl;
    x--;
} while (x > 0);
```

## Break and Continue

Same keywords in both languages: `break` and `continue`

**Python:**
```python
for i in range(10):
    if i == 5:
        break       # Exit loop
    if i % 2 == 0:
        continue    # Skip to next iteration
    print(i)
```

**C++:**
```cpp
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;      // Exit loop
    }
    if (i % 2 == 0) {
        continue;   // Skip to next iteration
    }
    std::cout << i << std::endl;
}
```

---

[← Previous: Operators](03-operators.md) | [Next: Functions →](05-functions.md)
