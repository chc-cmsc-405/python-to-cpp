# C++ Reading Guide by Phase

This guide maps the Python-to-C++ reference materials to the course phases. Read the assigned sections **before** watching the async videos—they'll provide context and help you recognize familiar patterns.

---

## Phase 1: Basics (Session 2 Async)

**Topics:** Variables, types, I/O, operators

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [01-basics](01-basics.md) | All | Comments, Hello World, cout/cin, variables |
| [02-data-types](02-data-types.md) | All | int, double, string, bool, type conversion |
| [03-operators](03-operators.md) | All | Arithmetic, comparison, logical (&&, \|\|, !) |

**Key takeaways:**
- Every variable needs a type declaration
- Use `std::cout <<` instead of `print()`
- Use `std::cin >>` instead of `input()`
- Semicolons are required after every statement
- Use `&&`, `||`, `!` instead of `and`, `or`, `not`

---

## Phase 2: Collections (Session 4-5)

**Topics:** Arrays, vectors, strings, file I/O

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [04-control-flow](04-control-flow.md) | For Loop section | Traditional for loop, range-based for |
| [05-functions](05-functions.md) | All | Function definition, parameters, pass by reference |
| [06-data-structures](06-data-structures.md) | Vectors, Strings | vector<T>, push_back, size, string operations |
| [07-io-streams](07-io-streams.md) | All | getline, ifstream, ofstream, stringstream |

**Key takeaways:**
- `std::vector<int>` is like Python's list (but single type only)
- Use `push_back()` instead of `append()`
- Use `size()` instead of `len()`
- Range-based for: `for (int x : vec)` is like `for x in list`
- `getline()` works on any input stream (cin or file)
- File I/O uses `ifstream` and `ofstream`

---

## Phase 3: Custom Types (Session 6 Async)

**Topics:** Structs, passing structs to functions

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [08-custom-types](08-custom-types.md) | Structs section only | struct definition, member access, passing to functions |

**Note:** Stop after the "Structs vs Classes" table. We'll cover classes in the in-person session.

**Key takeaways:**
- Structs group related data (like Python dataclasses)
- Access members with dot notation: `student.name`
- Use `const Student&` for read-only function parameters
- Use `Student&` when you need to modify the struct
- `vector<Student>` holds a collection of structs

---

## Phase 4: Pointers (Session 8 Async)

**Topics:** Pointers, references, arrow operator

| Read | Sections | Key Concepts |
|------|----------|--------------|
| [09-unique-features](09-unique-features.md) | Pointers, References, Arrow Operator, Pointers vs References | &, *, ->, nullptr |

**Note:** Stop after "Arrow Operator" section. We'll cover memory management (new/delete) in the in-person session.

**Key takeaways:**
- `&x` gives the address of x
- `*ptr` gives the value at an address (dereference)
- `ptr->member` accesses a member through a pointer
- References (`int& ref`) are aliases—they can't be null or reassigned
- Pointers (`int* ptr`) can be null, reassigned, and used for dynamic allocation

---

## Quick Reference: What to Read When

| Phase | Session | Read Before Class |
|-------|---------|-------------------|
| 1 | S2 (Mon) | 01-basics, 02-data-types, 03-operators |
| 2 | S4 (Mon) | 04-control-flow (loops), 05-functions, 06-data-structures, 07-io-streams |
| 3 | S6 (Mon) | 08-custom-types (structs only) |
| 4 | S8 (Mon) | 09-unique-features (pointers/references) |

---

## Full Reference

For complete coverage or later review, all sections are available:

| Guide | Topics |
|-------|--------|
| [01-basics](01-basics.md) | Comments, Hello World, console I/O, variables, constants |
| [02-data-types](02-data-types.md) | Types, type conversion |
| [03-operators](03-operators.md) | Arithmetic, comparison, logical |
| [04-control-flow](04-control-flow.md) | If/else, for, while, break/continue |
| [05-functions](05-functions.md) | Functions, parameters, pass by reference |
| [06-data-structures](06-data-structures.md) | Vectors, maps, strings |
| [07-io-streams](07-io-streams.md) | File I/O, getline, stringstream |
| [08-custom-types](08-custom-types.md) | Structs, classes, inheritance |
| [09-unique-features](09-unique-features.md) | Pointers, references, memory, headers |
