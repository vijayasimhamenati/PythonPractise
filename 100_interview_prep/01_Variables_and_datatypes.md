# Python Variables and Datatypes: Interview Prep Guide

## 1. Quick Concept Primer

### Variables & Memory Management

- **Dynamic Typing:** Python is dynamically typed. You don't need to declare a variable's type explicitly; the type is inferred at runtime based on the assigned value.
- **Reference System:** Variables in Python are references (pointers) to objects stored in memory, not the storage locations themselves.
- **Mutability:** Objects are classified based on whether their values can change after creation:
  - **Mutable:** `list`, `dict`, `set`, `bytearray`
  - **Immutable:** `int`, `float`, `str`, `tuple`, `bool`, `frozenset`
- **Garbage Collection:** Python manages memory automatically using **reference counting** and a **cyclic garbage collector**.

### Core Built-in Datatypes

1. **Numeric:** `int`, `float`, `complex`
2. **Sequence:** `str`, `list`, `tuple`, `range`
3. **Mapping:** `dict`
4. **Set:** `set`, `frozenset`
5. **Boolean:** `bool` (`True`, `False`)
6. **None:** `NoneType` (`None`)

---

## 2. Code Implementations & Core Patterns

### Variable Assignment & Reference Check (`is` vs `==`)

```python
# '==' checks for value equality
# 'is' checks for memory address identity (same object in memory)

a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)  # True (same values)
print(a is b)  # False (different objects in memory)

# Python small integer caching (-5 to 256) and string interning
x = 256
y = 256
print(x is y)  # True (cached integers)

p = 1000
q = 1000
print(p is q)  # False (depends on Python implementation/runtime)
```

### Mutability Demonstration

```python
# Immutable: String modification creates a new object
s = "hello"
# s[0] = 'H'  # TypeError: 'str' object does not support item assignment

# Mutable: List modification happens in-place
my_list = [1, 2, 3]
print(id(my_list))
my_list.append(4)
print(id(my_list))  # ID remains the same
```

---

## 3. Top Interview Questions & Answers

### Q1: What is the difference between `is` and `==` in Python?

- **Answer:**
  - `==` compares the **values** of two objects to check if they are equal.
  - `is` compares the **memory addresses** (identity) to check if both variables point to the exact same object in memory.

### Q2: Explain Python's Integer Caching (Small Integer Intering).

- **Answer:**
  Python pre-allocates a small range of integer objects from `-5` to `256` at startup for performance optimization. Whenever you create an integer within this range, Python returns a reference to the existing cached object rather than creating a new one in memory.

### Q3: What happens when you pass a mutable object (like a list) into a function?

- **Answer:**
  It is passed by **assignment** (often referred to as pass-by-object-reference). If the function modifies the mutable object in-place (e.g., using `.append()` or `[]=` assignment), the changes **will** reflect outside the function scope. Rebinding the variable name inside the function (`my_list = [1, 2]`) does not affect the original reference outside.

### Q4: How does Python handle memory management?

- **Answer:**
  Python uses two primary mechanisms:
  1. **Reference Counting:** Tracks how many references point to an object. When the count drops to zero, the memory is deallocated immediately.
  2. **Garbage Collector (Generational GC):** Handles reference cycles (e.g., object A references object B and B references A) where reference counts never drop to zero.

---

## 4. Common Pitfalls & Edge Cases

- **Mutable Default Arguments:** Never use a mutable object (like a list or dict) as a default argument in a function definition.
  ```python
  # BAD:
  def add_item(item, lst=[]):
      lst.append(item)
      return lst
  # The list 'lst' persists across function calls! Use `None` instead.
  ```
- **Shallow Copy vs Deep Copy:** Using slicing `[:]` or `.copy()` only performs a shallow copy. Nested objects will still point to the original references. Use `copy.deepcopy()` for fully independent nested structures.
