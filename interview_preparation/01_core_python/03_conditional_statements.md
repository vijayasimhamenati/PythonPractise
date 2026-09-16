# Python Conditional Statements: Interview Prep Guide

## 1. Quick Concept Primer

### Core Conditionals

- **Keywords:** `if`, `elif`, `else`. Python evaluates these in order from top to bottom.
- **Indentation:** Python uses whitespace (indentation) to define blocks of code instead of curly braces `{}`.
- **The `pass` Statement:** A null operation used as a placeholder when a statement is syntactically required but you want no code to execute.

### Truthiness and Falsiness

In Python, you don't need to explicitly compare to `True` or `False`. Every object has an inherent boolean value.

- **Falsy Values:** Evaluate to `False`. Includes `None`, `False`, zeros of any numeric type (`0`, `0.0`), empty sequences/collections (`''`, `[]`, `()`, `{}`), and custom objects that implement `__bool__` or `__len__` returning `False` or `0`.
- **Truthy Values:** Everything else evaluates to `True`.

### Structural Pattern Matching (Python 3.10+)

- Python introduced `match` and `case` statements, similar to `switch` in other languages but much more powerful. It allows for matching structure, type, and specific values.

---

## 2. Code Implementations & Core Patterns

### Basic Control Flow & Truthiness

```python
user_input = ""

# Idiomatic Python: checking truthiness directly
if not user_input:
    print("Input is empty!")  # This will execute because "" is falsy
elif user_input == "admin":
    print("Welcome admin.")
else:
    print("Welcome user.")
```

### Dictionary Mapping (Pre-3.10 Switch Statement Alternative)

```python
# Before Python 3.10, dictionaries were the idiomatic way to handle multiple conditions
def get_status_message(status_code):
    status_map = {
        200: "OK",
        404: "Not Found",
        500: "Internal Server Error"
    }
    # Use .get() with a default fallback
    return status_map.get(status_code, "Unknown Status")

print(get_status_message(404))  # Output: Not Found
```

### Structural Pattern Matching (Python 3.10+)

```python
def process_data(data):
    match data:
        case {"type": "user", "id": user_id}:
            print(f"Processing user {user_id}")
        case [x, y] if x == y:
            # Match an iterable of length 2 where both elements are equal (using a guard)
            print("Matched a pair of identical items")
        case _:
            # The underscore acts as a wildcard/default case
            print("Data format unknown")

process_data({"type": "user", "id": 105})
process_data([5, 5])
```

---

## 3. Top Interview Questions & Answers

### Q1: Does Python have block-level scoping for `if` statements?

- **Answer:**
  No. Variables declared inside an `if`, `elif`, or `else` block are accessible outside of that block, provided the code path defining them was executed. Python's scope is resolved at the function or module level, not the block level.

### Q2: How do you write an inline `if` statement?

- **Answer:**
  Using Python's ternary operator (conditional expression). The syntax is `[on_true] if [expression] else [on_false]`. For example: `x = 10 if condition else 20`.

### Q3: Why is checking `if my_list:` preferred over `if len(my_list) > 0:`?

- **Answer:**
  Checking `if my_list:` relies on Python's built-in truthiness evaluation, which is more idiomatic (PEP 8 recommended) and slightly faster. Empty collections are inherently falsy.

---

## 4. Common Pitfalls & Edge Cases

- **UnboundLocalError:** Because variables leak out of conditional blocks, if a condition is not met and you try to use a variable defined only within that block, Python will throw an error.
  ```python
  flag = False
  if flag:
      result = "Success"
  # print(result) # NameError: name 'result' is not defined
  ```
  _Solution:_ Always initialize variables before the conditional block if they will be used later.
- **Chaining `elif` forever vs Dictionary Mapping:** Writing 10 `elif` statements is an anti-pattern. If you are matching single values (like status codes or command strings), use a dictionary mapping or Python 3.10+ `match/case` for cleaner, more maintainable code.
