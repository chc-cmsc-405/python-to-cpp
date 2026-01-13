# 03 - Operators

[← Back to C++ Guide](README.md)

Most operators work the same in C++ as in Python, but there are a few important differences. The biggest gotcha is integer division: `7 / 2` gives `3` in C++ (not `3.5`). C++ also uses symbols for logical operators (`&&`, `||`, `!`) instead of words (`and`, `or`, `not`), and there's no `**` operator for exponents—use `pow()` from the `<cmath>` library instead.

---

## Arithmetic

| Operation | Python | C++ |
|-----------|--------|-----|
| Addition | `a + b` | `a + b` |
| Subtraction | `a - b` | `a - b` |
| Multiplication | `a * b` | `a * b` |
| Division | `a / b` (float result) | `a / b` (int if both int!) |
| Floor division | `a // b` | `a / b` (for integers) |
| Modulus | `a % b` | `a % b` |
| Exponent | `a ** b` | `pow(a, b)` (requires `#include <cmath>`) |

## Important: Integer Division

This is a common gotcha when moving from Python to C++:

**Python:**
```python
7 / 2   # = 3.5 (always float)
7 // 2  # = 3 (floor division)
```

**C++:**
```cpp
7 / 2   // = 3 (integer division!)
7.0 / 2 // = 3.5 (float division)
```

In C++, if both operands are integers, `/` performs integer division. To get a float result, at least one operand must be a float/double.

## Comparison

| Operation | Python | C++ |
|-----------|--------|-----|
| Equal | `==` | `==` |
| Not equal | `!=` | `!=` |
| Less than | `<` | `<` |
| Greater than | `>` | `>` |
| Less or equal | `<=` | `<=` |
| Greater or equal | `>=` | `>=` |

## Logical

| Operation | Python | C++ |
|-----------|--------|-----|
| And | `and` | `&&` |
| Or | `or` | `\|\|` |
| Not | `not` | `!` |

**Python:**
```python
if x > 0 and y > 0:
    print("Both positive")
if not found:
    print("Not found")
```

**C++:**
```cpp
if (x > 0 && y > 0) {
    std::cout << "Both positive" << std::endl;
}
if (!found) {
    std::cout << "Not found" << std::endl;
}
```

---

[← Previous: Data Types](02-data-types.md) | [Next: Control Flow →](04-control-flow.md)
