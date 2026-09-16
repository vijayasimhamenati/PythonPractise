# Python Operators and Expressions: Interview Prep Guide

## 1. Quick Concept Primer

### Types of Operators

- **Arithmetic:** `+`, `-`, `*`, `/` (float division), `//` (floor division), `%` (modulo), `**` (exponentiation).
- **Comparison (Relational):** `==`, `!=`, `>`, `<`, `>=`, `<=`. Python supports chaining (e.g., `1 < x < 10`).
- **Logical:** `and`, `or`, `not`. These are evaluated using **short-circuit logic**.
- **Bitwise:** `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (Left Shift), `>>` (Right Shift). Often used in algorithmic problem-solving.
- **Identity:** `is`, `is not`. Checks if two variables point to the same memory address.
- **Membership:** `in`, `not in`. Checks for presence in sequences (strings, lists, tuples) or collections (sets, dictionaries).

### Expressions & Precedence

- An **expression** is any combination of variables, constants, and operators that evaluates to a single value.
- **Operator Precedence (PEMDAS roughly applies):**
  1. Parentheses `()`
  2. Exponentiation `**`
  3. Unary plus/minus, Bitwise NOT `+x`, `-x`, `~x`
  4. Multiplication, Division, Modulo `*`, `/`, `//`, `%`
  5. Addition, Subtraction `+`, `-`
  6. Bitwise Shifts `<<`, `>>`
  7. Bitwise AND `&`, then XOR `^`, then OR `|`
  8. Comparisons, Identity, Membership `==`, `!=`, `>`, `<`, `is`, `in`
  9. Logical NOT `not`, then AND `and`, then OR `or`

---

## 2. Code Implementations & Core Patterns

### Short-Circuit Evaluation

```python
def expensive_operation():
    print("Expensive operation ran!")
    return True

# 'or' short-circuits if the first operand is True
x = True or expensive_operation()  # expensive_operation() is NOT called

# 'and' short-circuits if the first operand is False
y = False and expensive_operation() # expensive_operation() is NOT called
```

### The Ternary Operator (Conditional Expression)

```python
# Syntax: [value_if_true] if [condition] else [value_if_false]
age = 25
status = "Adult" if age >= 18 else "Minor"
print(status)  # Output: Adult
```

### Chained Comparisons

```python
x = 5
# Instead of: x > 0 and x < 10
print(0 < x < 10)  # True, evaluated internally as (0 < x) and (x < 10)
```

### Floor Division & Modulo Edge Cases

```python
# Floor division always rounds DOWN (towards negative infinity)
print(10 // 3)   # 3
print(-10 // 3)  # -4 (Notice it's not -3!)

# Modulo always takes the sign of the divisor in Python
print(-10 % 3)   # 2
```

---

## 3. Top Interview Questions & Answers

### Q1: What is the difference between `/` and `//` in Python?

- **Answer:**
  - `/` performs "true division" and always returns a `float`, even if the numbers divide evenly (e.g., `4 / 2` is `2.0`).
  - `//` performs "floor division". It returns an `int` (if both operands are ints) and always rounds the result down to the next smallest integer (towards negative infinity).

### Q2: What is short-circuit evaluation in logical operators?

- **Answer:**
  Python stops evaluating logical expressions as soon as the result is determined.
  - For `A and B`, if `A` is `False`, Python immediately evaluates the whole expression as `False` without checking `B`.
  - For `A or B`, if `A` is `True`, Python immediately evaluates the whole expression as `True` without checking `B`.

### Q3: What is the difference between logical `and` / `or` and bitwise `&` / `|`?

- **Answer:**
  - `and` / `or` are used for boolean logic, employ short-circuiting, and return the actual operand value that decided the outcome.
  - `&` / `|` are bitwise operators that operate on numbers at the binary level. They do not short-circuit. (Note: in libraries like Pandas/NumPy, `&` and `|` are overloaded for element-wise boolean operations on arrays).

---

## 4. Common Pitfalls & Edge Cases

- **Floating Point Precision Issues:**
  ```python
  print(0.1 + 0.2 == 0.3)  # False!
  # Why? Because 0.1 + 0.2 evaluates to 0.30000000000000004 due to binary floating-point representation. Use `math.isclose()` for float comparisons.
  ```
- **Bitwise NOT (`~`) on Integers:**
  The bitwise NOT operator doesn't just flip bits in an intuitive way due to Two's Complement representation. `~x` always evaluates to `-(x + 1)`.
  ```python
  print(~5)  # -6
  ```
