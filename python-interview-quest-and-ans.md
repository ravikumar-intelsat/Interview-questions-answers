# Python Interview Questions and Answers

> Based on [roadmap.sh/python](https://roadmap.sh/python) - Comprehensive Interview Preparation Guide

---

## Table of Contents

1. [Python Basics](#python-basics)
2. [Variables and Data Types](#variables-and-data-types)
3. [Operators](#operators)
4. [Control Flow](#control-flow)
5. [Functions](#functions)
6. [Data Structures](#data-structures)
7. [Object-Oriented Programming (OOP)](#object-oriented-programming-oop)
8. [Exception Handling](#exception-handling)
9. [File I/O Operations](#file-io-operations)
10. [Modules and Packages](#modules-and-packages)
11. [Decorators](#decorators)
12. [Generators and Iterators](#generators-and-iterators)
13. [Comprehensions](#comprehensions)
14. [Lambda Functions](#lambda-functions)
15. [Regular Expressions](#regular-expressions)
16. [Database Operations](#database-operations)
17. [Web Development](#web-development)
18. [Testing](#testing)
19. [Async/Await](#asyncawait)
20. [Context Managers](#context-managers)
21. [Memory Management](#memory-management)
22. [Advanced Topics](#advanced-topics)

---

## Python Basics

### Q1. What is Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Basics, Language Fundamentals

**Answer:**

Python is a high-level, interpreted, general-purpose programming language created by Guido van Rossum and first released in 1991. It emphasizes code readability and simplicity.

**Key Features:**
- **Interpreted:** Code is executed line by line (no compilation needed)
- **Dynamically Typed:** Variable types are determined at runtime
- **Object-Oriented:** Supports OOP paradigms
- **High-Level:** Abstracts low-level details
- **Cross-Platform:** Runs on Windows, macOS, Linux
- **Extensive Standard Library:** Rich built-in modules
- **Large Ecosystem:** Third-party packages via PyPI

**Use Cases:**
- Web development (Django, Flask, FastAPI)
- Data science and analytics (Pandas, NumPy)
- Machine Learning (TensorFlow, PyTorch)
- Automation and scripting
- Backend development
- API development

**Example:**
```python
print("Hello, World!")
```

---

### Q2. What are the key differences between Python 2 and Python 3? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Language Fundamentals, Version Differences

**Answer:**

**Major Differences:**

1. **Print Statement:**
   - Python 2: `print "Hello"` (statement)
   - Python 3: `print("Hello")` (function)

2. **Integer Division:**
   - Python 2: `5 / 2 = 2` (integer division)
   - Python 3: `5 / 2 = 2.5` (true division)
   - Python 2: `5 // 2 = 2` (floor division)
   - Python 3: `5 // 2 = 2` (floor division)

3. **Unicode:**
   - Python 2: Strings are bytes by default
   - Python 3: Strings are Unicode by default

4. **xrange vs range:**
   - Python 2: `xrange()` returns iterator, `range()` returns list
   - Python 3: Only `range()` exists (returns iterator)

5. **Exception Syntax:**
   - Python 2: `except Exception, e:`
   - Python 3: `except Exception as e:`

6. **Input Function:**
   - Python 2: `raw_input()` returns string, `input()` evaluates
   - Python 3: Only `input()` exists (returns string)

**Note:** Python 2 reached end-of-life on January 1, 2020. All new projects should use Python 3.

---

### Q3. What is PEP 8? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Code Style, Best Practices

**Answer:**

PEP 8 is the official style guide for Python code. It provides conventions for writing readable Python code.

**Key Guidelines:**

1. **Indentation:** Use 4 spaces (not tabs)
2. **Line Length:** Maximum 79 characters (99 for comments)
3. **Imports:** One import per line, grouped (stdlib, third-party, local)
4. **Naming:**
   - Functions/variables: `snake_case`
   - Classes: `PascalCase`
   - Constants: `UPPER_SNAKE_CASE`
   - Private: `_leading_underscore`
5. **Whitespace:** Use spaces around operators, after commas
6. **Comments:** Complete sentences, start with capital letter

**Example:**
```python
# Good
def calculate_total(items):
    """Calculate total price of items."""
    total = sum(item.price for item in items)
    return total

# Bad
def calculateTotal(items):
    total=sum(item.price for item in items)
    return total
```

**Tools:** Use `flake8`, `black`, or `pylint` to check PEP 8 compliance.

---

## Variables and Data Types

### Q4. What are the different data types in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Variables, Data Types, Constants

**Answer:**

Python has several built-in data types:

**1. Numeric Types:**
```python
# Integer
x = 10
type(x)  # <class 'int'>

# Float
y = 10.5
type(y)  # <class 'float'>

# Complex
z = 3 + 4j
type(z)  # <class 'complex'>
```

**2. Sequence Types:**
```python
# String
s = "Hello"
type(s)  # <class 'str'>

# List (mutable)
lst = [1, 2, 3]
type(lst)  # <class 'list'>

# Tuple (immutable)
tup = (1, 2, 3)
type(tup)  # <class 'tuple'>

# Range
r = range(5)
type(r)  # <class 'range'>
```

**3. Set Types:**
```python
# Set (mutable, unordered, unique)
s = {1, 2, 3}
type(s)  # <class 'set'>

# Frozenset (immutable)
fs = frozenset([1, 2, 3])
type(fs)  # <class 'frozenset'>
```

**4. Mapping Type:**
```python
# Dictionary
d = {"key": "value"}
type(d)  # <class 'dict'>
```

**5. Boolean Type:**
```python
b = True
type(b)  # <class 'bool'>
```

**6. Binary Types:**
```python
# Bytes (immutable)
b = b"hello"
type(b)  # <class 'bytes'>

# Bytearray (mutable)
ba = bytearray(b"hello")
type(ba)  # <class 'bytearray'>

# Memoryview
mv = memoryview(b"hello")
type(mv)  # <class 'memoryview'>
```

**7. None Type:**
```python
n = None
type(n)  # <class 'NoneType'>
```

---

### Q5. What is the difference between mutable and immutable objects? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Variables, Data Types, Memory Management

**Answer:**

**Mutable objects** can be modified after creation, while **immutable objects** cannot.

**Immutable Types:**
- `int`, `float`, `complex`
- `str`
- `tuple`
- `frozenset`
- `bytes`

**Mutable Types:**
- `list`
- `dict`
- `set`
- `bytearray`

**Example:**
```python
# Immutable - creates new object
x = "Hello"
y = x
x = x + " World"  # x is now "Hello World", y is still "Hello"
print(x)  # "Hello World"
print(y)  # "Hello"

# Mutable - modifies existing object
lst1 = [1, 2, 3]
lst2 = lst1
lst1.append(4)  # Modifies the same object
print(lst1)  # [1, 2, 3, 4]
print(lst2)  # [1, 2, 3, 4] (same object!)

# To create a copy of mutable object
lst3 = lst1.copy()  # or list(lst1) or lst1[:]
lst3.append(5)
print(lst1)  # [1, 2, 3, 4]
print(lst3)  # [1, 2, 3, 4, 5]
```

**Implications:**
- Immutable objects are hashable (can be dictionary keys)
- Mutable objects cannot be dictionary keys
- Immutable objects are thread-safe
- String concatenation creates new objects (use `join()` for efficiency)

---

### Q6. What are constants in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Variables, Constants

**Answer:**

Python doesn't have true constants, but by convention, variables in `UPPER_SNAKE_CASE` are treated as constants.

**Convention:**
```python
# Constants (convention, not enforced)
PI = 3.14159
MAX_SIZE = 100
DEFAULT_TIMEOUT = 30

# Module-level constants
class Config:
    DATABASE_URL = "postgresql://localhost/db"
    API_KEY = "secret_key"
```

**Using `enum` for constants:**
```python
from enum import Enum

class Status(Enum):
    PENDING = 1
    APPROVED = 2
    REJECTED = 3

# Usage
status = Status.PENDING
print(status.value)  # 1
```

**Note:** Python doesn't prevent modification of "constants". It's a convention, not a language feature.

---

### Q7. Explain variable scope in Python. (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Variables, Scope, Functions

**Answer:**

Python has four levels of scope:

1. **Local (L):** Inside current function
2. **Enclosing (E):** In enclosing functions (non-local)
3. **Global (G):** At module level
4. **Built-in (B):** Built-in names

**Example:**
```python
x = "global"  # Global scope

def outer():
    x = "outer"  # Enclosing scope
    
    def inner():
        x = "inner"  # Local scope
        print(x)  # "inner"
    
    inner()
    print(x)  # "outer"

outer()
print(x)  # "global"
```

**`global` keyword:**
```python
count = 0

def increment():
    global count  # Declare global
    count += 1

increment()
print(count)  # 1
```

**`nonlocal` keyword:**
```python
def outer():
    x = 10
    
    def inner():
        nonlocal x  # Reference enclosing scope
        x = 20
    
    inner()
    print(x)  # 20

outer()
```

**LEGB Rule:** Python searches for names in Local → Enclosing → Global → Built-in order.

---

## Operators

### Q8. What are the different types of operators in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Operators

**Answer:**

**1. Arithmetic Operators:**
```python
a, b = 10, 3
a + b   # 13 (addition)
a - b   # 7 (subtraction)
a * b   # 30 (multiplication)
a / b   # 3.333... (division)
a // b  # 3 (floor division)
a % b   # 1 (modulus)
a ** b  # 1000 (exponentiation)
```

**2. Comparison Operators:**
```python
a == b  # False (equal)
a != b  # True (not equal)
a < b   # False (less than)
a > b   # True (greater than)
a <= b  # False (less than or equal)
a >= b  # True (greater than or equal)
```

**3. Logical Operators:**
```python
True and False  # False
True or False   # True
not True        # False
```

**4. Assignment Operators:**
```python
x = 5
x += 3   # x = x + 3 (8)
x -= 2   # x = x - 2 (6)
x *= 2   # x = x * 2 (12)
x /= 3   # x = x / 3 (4.0)
```

**5. Identity Operators:**
```python
a is b      # True if same object
a is not b  # True if different objects

x = [1, 2, 3]
y = [1, 2, 3]
x == y   # True (same values)
x is y   # False (different objects)
```

**6. Membership Operators:**
```python
x in [1, 2, 3]        # True
x not in [1, 2, 3]    # False
"a" in "apple"        # True
```

**7. Bitwise Operators:**
```python
a & b   # AND
a | b   # OR
a ^ b   # XOR
~a      # NOT
a << 2  # Left shift
a >> 2  # Right shift
```

---

### Q9. What is the difference between `==` and `is`? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Operators, Memory Management

**Answer:**

- `==` compares **values** (equality)
- `is` compares **object identity** (same object in memory)

**Example:**
```python
# Same values, different objects
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)   # True (same values)
print(a is b)   # False (different objects)

# Same object
c = a
print(a is c)   # True (same object)

# Integers (small integers are cached)
x = 256
y = 256
print(x is y)   # True (cached)

# Large integers (not cached)
x = 257
y = 257
print(x is y)   # False (different objects, but == is True)
```

**When to use:**
- Use `==` for value comparison
- Use `is` for checking `None`, `True`, `False`, or object identity

**Best Practice:**
```python
# Good
if x is None:
    pass

# Avoid
if x == None:  # Use 'is' instead
    pass
```

---

## Control Flow

### Q10. Explain if-else statements in Python. (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Control Flow

**Answer:**

**Basic Syntax:**
```python
if condition:
    # code block
elif another_condition:
    # code block
else:
    # code block
```

**Example:**
```python
age = 20

if age < 18:
    print("Minor")
elif age < 65:
    print("Adult")
else:
    print("Senior")
```

**Ternary Operator:**
```python
# Traditional
if x > 0:
    result = "positive"
else:
    result = "negative"

# Ternary
result = "positive" if x > 0 else "negative"
```

**Multiple Conditions:**
```python
if x > 0 and x < 100:
    print("Valid range")

if x < 0 or x > 100:
    print("Out of range")
```

---

### Q11. What are the different types of loops in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Control Flow, Loops

**Answer:**

**1. for Loop:**
```python
# Iterate over sequence
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# Iterate over list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# With index
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Iterate over dictionary
person = {"name": "John", "age": 30}
for key, value in person.items():
    print(f"{key}: {value}")
```

**2. while Loop:**
```python
count = 0
while count < 5:
    print(count)
    count += 1
```

**3. Loop Control:**
```python
# break - exit loop
for i in range(10):
    if i == 5:
        break
    print(i)  # 0, 1, 2, 3, 4

# continue - skip iteration
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)  # 1, 3, 5, 7, 9

# else with loops (executes if loop completes normally)
for i in range(5):
    print(i)
else:
    print("Loop completed")  # Executes after loop
```

**4. Nested Loops:**
```python
for i in range(3):
    for j in range(3):
        print(f"({i}, {j})")
```

---

## Functions

### Q12. How do you define and call functions in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Functions

**Answer:**

**Function Definition:**
```python
def greet(name):
    """Return a greeting message."""
    return f"Hello, {name}!"

# Call function
message = greet("Alice")
print(message)  # "Hello, Alice!"
```

**Function with Default Arguments:**
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Alice")              # "Hello, Alice!"
greet("Bob", "Hi")          # "Hi, Bob!"
```

**Function with Multiple Return Values:**
```python
def divide(a, b):
    quotient = a // b
    remainder = a % b
    return quotient, remainder

q, r = divide(10, 3)
print(q, r)  # 3 1
```

**Function with Type Hints (Python 3.5+):**
```python
def add(a: int, b: int) -> int:
    return a + b
```

---

### Q13. What is the difference between `*args` and `**kwargs`? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Functions, Arguments

**Answer:**

- `*args` collects extra positional arguments as a tuple
- `**kwargs` collects extra keyword arguments as a dictionary

**Example:**
```python
def example_function(required, *args, **kwargs):
    print(f"Required: {required}")
    print(f"Args: {args}")
    print(f"Kwargs: {kwargs}")

example_function(1, 2, 3, 4, name="Alice", age=30)
# Required: 1
# Args: (2, 3, 4)
# Kwargs: {'name': 'Alice', 'age': 30}
```

**Unpacking:**
```python
def add(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
result = add(*numbers)  # Unpacks list

person = {"name": "Alice", "age": 30}
def greet(name, age):
    return f"{name} is {age} years old"

greet(**person)  # Unpacks dictionary
```

**Common Use Cases:**
```python
# Decorators
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function")
        result = func(*args, **kwargs)
        print("After function")
        return result
    return wrapper

# Function forwarding
def wrapper_function(*args, **kwargs):
    return original_function(*args, **kwargs)
```

---

### Q14. What are lambda functions? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Functions, Lambda

**Answer:**

Lambda functions are anonymous functions defined with the `lambda` keyword.

**Syntax:**
```python
lambda arguments: expression
```

**Example:**
```python
# Regular function
def add(x, y):
    return x + y

# Lambda function
add = lambda x, y: x + y

# Usage
result = add(3, 5)  # 8
```

**Common Use Cases:**

**1. With map():**
```python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
# [1, 4, 9, 16, 25]
```

**2. With filter():**
```python
numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, numbers))
# [2, 4, 6]
```

**3. With sorted():**
```python
people = [("Alice", 30), ("Bob", 25), ("Charlie", 35)]
sorted_by_age = sorted(people, key=lambda x: x[1])
# [("Bob", 25), ("Alice", 30), ("Charlie", 35)]
```

**4. In list comprehensions:**
```python
# Not recommended - use list comprehension instead
result = [(lambda x: x * 2)(x) for x in range(5)]
# Better:
result = [x * 2 for x in range(5)]
```

**Limitations:**
- Can only contain expressions, not statements
- No annotations
- Single expression only

---

### Q15. What is a closure in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Functions, Closures

**Answer:**

A closure is a function that remembers values from its enclosing scope even after the outer function has finished executing.

**Example:**
```python
def outer_function(x):
    # Enclosing scope
    def inner_function(y):
        # Inner function uses x from outer scope
        return x + y
    return inner_function

# Create closure
add_five = outer_function(5)
result = add_five(3)  # 8
```

**Practical Example:**
```python
def make_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))   # 10
print(triple(5))   # 15
```

**Common Use Case - Decorators:**
```python
def counter(func):
    count = 0  # Enclosed variable
    
    def wrapper(*args, **kwargs):
        nonlocal count
        count += 1
        print(f"Function called {count} times")
        return func(*args, **kwargs)
    
    return wrapper

@counter
def greet(name):
    return f"Hello, {name}!"

greet("Alice")  # Function called 1 times
greet("Bob")    # Function called 2 times
```

**Key Points:**
- Closures capture variables by reference
- Use `nonlocal` to modify enclosed variables
- Useful for function factories and decorators

---

## Data Structures

### Q16. What are lists in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Data Structures, Lists

**Answer:**

Lists are ordered, mutable collections of items.

**Creating Lists:**
```python
# Empty list
lst = []
lst = list()

# With items
lst = [1, 2, 3]
lst = ["apple", "banana", "cherry"]
lst = [1, "hello", 3.14, True]  # Mixed types
```

**Common Operations:**
```python
lst = [1, 2, 3]

# Access
lst[0]        # 1 (first element)
lst[-1]        # 3 (last element)

# Modify
lst[0] = 10    # [10, 2, 3]

# Add
lst.append(4)           # [10, 2, 3, 4]
lst.insert(1, 5)        # [10, 5, 2, 3, 4]
lst.extend([6, 7])      # [10, 5, 2, 3, 4, 6, 7]

# Remove
lst.remove(5)           # Remove first occurrence
lst.pop()               # Remove and return last item
lst.pop(0)              # Remove and return item at index
del lst[0]              # Delete item at index

# Other
lst.index(2)            # Find index of value
lst.count(2)            # Count occurrences
lst.reverse()           # Reverse in place
lst.sort()              # Sort in place
sorted(lst)             # Return sorted copy
len(lst)                # Length
```

**List Slicing:**
```python
lst = [0, 1, 2, 3, 4, 5]
lst[1:4]      # [1, 2, 3]
lst[:3]       # [0, 1, 2]
lst[3:]       # [3, 4, 5]
lst[::2]      # [0, 2, 4] (step)
lst[::-1]     # [5, 4, 3, 2, 1, 0] (reverse)
```

---

### Q17. What are tuples in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Data Structures, Tuples

**Answer:**

Tuples are ordered, immutable collections of items.

**Creating Tuples:**
```python
# Empty tuple
tup = ()
tup = tuple()

# With items
tup = (1, 2, 3)
tup = 1, 2, 3  # Parentheses optional
tup = (1,)     # Single item (comma required)

# From list
tup = tuple([1, 2, 3])
```

**Operations:**
```python
tup = (1, 2, 3)

# Access
tup[0]        # 1
tup[-1]       # 3

# Cannot modify (immutable)
# tup[0] = 10  # Error!

# Concatenation
tup2 = tup + (4, 5)  # (1, 2, 3, 4, 5)

# Unpacking
a, b, c = tup  # a=1, b=2, c=3

# Methods
tup.count(2)   # Count occurrences
tup.index(2)   # Find index
len(tup)       # Length
```

**Use Cases:**
- Return multiple values from functions
- Dictionary keys (must be immutable)
- Coordinates, records
- When immutability is desired

**Example:**
```python
def get_name_age():
    return "Alice", 30

name, age = get_name_age()

# Dictionary keys
locations = {
    (0, 0): "Origin",
    (1, 2): "Point A"
}
```

---

### Q18. What are dictionaries in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Data Structures, Dictionaries

**Answer:**

Dictionaries are unordered collections of key-value pairs (Python 3.7+ maintains insertion order).

**Creating Dictionaries:**
```python
# Empty
d = {}
d = dict()

# With items
d = {"name": "Alice", "age": 30}
d = dict(name="Alice", age=30)

# From list of tuples
d = dict([("name", "Alice"), ("age", 30)])
```

**Operations:**
```python
d = {"name": "Alice", "age": 30}

# Access
d["name"]              # "Alice"
d.get("name")          # "Alice"
d.get("city", "NYC")   # "NYC" (default if key missing)

# Modify
d["age"] = 31           # Update
d["city"] = "NYC"       # Add new
d.update({"city": "NYC", "country": "USA"})

# Remove
del d["age"]            # Delete key
value = d.pop("age")    # Remove and return value
d.popitem()             # Remove and return last item (3.7+)

# Iterate
for key in d:
    print(key, d[key])

for key, value in d.items():
    print(key, value)

for value in d.values():
    print(value)

# Methods
d.keys()                # View of keys
d.values()              # View of values
d.items()               # View of items
len(d)                  # Number of items
"name" in d             # Check key existence
```

**Dictionary Comprehensions:**
```python
# Create from list
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# With condition
evens = {x: x**2 for x in range(10) if x % 2 == 0}
```

---

### Q19. What are sets in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Data Structures, Sets

**Answer:**

Sets are unordered collections of unique elements.

**Creating Sets:**
```python
# Empty set (must use set(), not {})
s = set()
# s = {}  # This creates a dict, not a set!

# With items
s = {1, 2, 3}
s = set([1, 2, 3, 3])  # {1, 2, 3} (duplicates removed)
```

**Operations:**
```python
s = {1, 2, 3}

# Add/Remove
s.add(4)                # {1, 2, 3, 4}
s.remove(2)             # {1, 3, 4} (raises error if missing)
s.discard(2)            # {1, 3, 4} (no error if missing)
s.pop()                 # Remove and return arbitrary element
s.clear()               # Remove all

# Set Operations
a = {1, 2, 3}
b = {3, 4, 5}

a | b                   # Union: {1, 2, 3, 4, 5}
a & b                   # Intersection: {3}
a - b                   # Difference: {1, 2}
a ^ b                   # Symmetric difference: {1, 2, 4, 5}

# Methods
a.union(b)              # Same as a | b
a.intersection(b)       # Same as a & b
a.difference(b)         # Same as a - b
a.symmetric_difference(b)  # Same as a ^ b

# Check
1 in a                  # True
a.issubset(b)           # False
a.issuperset(b)         # False
a.isdisjoint(b)         # False
```

**Use Cases:**
- Remove duplicates
- Fast membership testing
- Mathematical set operations
- Finding unique elements

---

### Q20. Explain list vs tuple vs set vs dictionary. (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Data Structures, Comparison

**Answer:**

| Feature | List | Tuple | Set | Dictionary |
|---------|------|-------|-----|------------|
| **Ordered** | Yes | Yes | No (3.7+ insertion order) | Yes (3.7+) |
| **Mutable** | Yes | No | Yes | Yes |
| **Indexed** | Yes | Yes | No | Yes (by key) |
| **Duplicates** | Allowed | Allowed | No | Keys: No, Values: Yes |
| **Syntax** | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` | `{"k": "v"}` |
| **Use Case** | Ordered collection | Immutable sequence | Unique elements | Key-value pairs |

**When to Use:**

**List:** When you need ordered, mutable collection
```python
items = ["apple", "banana", "cherry"]
items.append("date")
```

**Tuple:** When you need immutable, ordered collection
```python
coordinates = (10, 20)  # Can't change
return name, age  # Multiple return values
```

**Set:** When you need unique elements, fast membership testing
```python
unique_numbers = {1, 2, 3, 3, 4}  # {1, 2, 3, 4}
if 2 in unique_numbers:  # O(1) lookup
    pass
```

**Dictionary:** When you need key-value mapping
```python
person = {"name": "Alice", "age": 30}
age = person["age"]  # O(1) lookup
```

---

## Object-Oriented Programming (OOP)

### Q21. What is a class in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, OOP, Classes

**Answer:**

A class is a blueprint for creating objects (instances).

**Basic Class:**
```python
class Person:
    # Class variable (shared by all instances)
    species = "Homo sapiens"
    
    # Constructor
    def __init__(self, name, age):
        # Instance variables
        self.name = name
        self.age = age
    
    # Instance method
    def greet(self):
        return f"Hello, I'm {self.name}"
    
    # Class method
    @classmethod
    def from_birth_year(cls, name, birth_year):
        age = 2024 - birth_year
        return cls(name, age)
    
    # Static method
    @staticmethod
    def is_adult(age):
        return age >= 18

# Create instance
person = Person("Alice", 30)
print(person.greet())  # "Hello, I'm Alice"

# Class method
person2 = Person.from_birth_year("Bob", 1994)

# Static method
print(Person.is_adult(25))  # True
```

**Key Concepts:**
- `self`: Reference to the instance
- `__init__`: Constructor method
- Instance variables: Unique to each instance
- Class variables: Shared by all instances
- Methods: Functions defined in class

---

### Q22. Explain inheritance in Python. (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Inheritance

**Answer:**

Inheritance allows a class to inherit attributes and methods from another class.

**Basic Inheritance:**
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # Call parent constructor
        self.breed = breed
    
    def speak(self):  # Override method
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# Usage
dog = Dog("Buddy", "Golden Retriever")
print(dog.name)      # "Buddy" (inherited)
print(dog.speak())   # "Woof!" (overridden)
```

**Multiple Inheritance:**
```python
class A:
    def method(self):
        return "A"

class B:
    def method(self):
        return "B"

class C(A, B):  # Multiple inheritance
    pass

c = C()
print(c.method())  # "A" (Method Resolution Order: C -> A -> B)
print(C.__mro__)   # Method Resolution Order
```

**Method Resolution Order (MRO):**
- Python uses C3 linearization algorithm
- Determines order of method lookup
- Access via `ClassName.__mro__`

---

### Q23. What is polymorphism in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Polymorphism

**Answer:**

Polymorphism allows objects of different types to be treated through the same interface.

**Duck Typing:**
```python
class Duck:
    def quack(self):
        return "Quack!"

class Dog:
    def quack(self):
        return "Woof! (pretending to quack)"

def make_sound(animal):
    return animal.quack()  # Doesn't care about type

duck = Duck()
dog = Dog()

print(make_sound(duck))  # "Quack!"
print(make_sound(dog))   # "Woof! (pretending to quack)"
```

**Method Overriding:**
```python
class Shape:
    def area(self):
        raise NotImplementedError

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2

# Polymorphic behavior
shapes = [Rectangle(5, 10), Circle(5)]
for shape in shapes:
    print(shape.area())  # Different implementations
```

**Operator Overloading:**
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)
    
    def __str__(self):
        return f"Point({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2  # Uses __add__
print(p3)     # Point(4, 6)
```

---

### Q24. What is encapsulation in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Encapsulation

**Answer:**

Encapsulation bundles data and methods together and restricts access using access modifiers.

**Access Modifiers:**
```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance          # Public
        self._account_number = "12345"  # Protected (convention)
        self.__pin = "0000"             # Private (name mangling)
    
    def deposit(self, amount):
        self.balance += amount
    
    def _validate(self):  # Protected method
        return True
    
    def __verify_pin(self, pin):  # Private method
        return self.__pin == pin

account = BankAccount(1000)
print(account.balance)        # OK (public)
print(account._account_number) # OK (convention, not enforced)
# print(account.__pin)         # Error! (name mangled to _BankAccount__pin)
print(account._BankAccount__pin)  # Works (but don't do this!)
```

**Property Decorator:**
```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature too low")
        self._celsius = value
    
    @property
    def fahrenheit(self):
        return self._celsius * 9/5 + 32

temp = Temperature(25)
print(temp.celsius)      # 25 (getter)
temp.celsius = 30        # (setter)
print(temp.fahrenheit)  # 86.0 (computed property)
```

---

### Q25. What are magic methods (dunder methods)? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Magic Methods

**Answer:**

Magic methods (dunder methods) are special methods with double underscores that define behavior for built-in operations.

**Common Magic Methods:**
```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    # String representation
    def __str__(self):
        return f"{self.title} by {self.author}"
    
    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"
    
    # Comparison
    def __eq__(self, other):
        return self.pages == other.pages
    
    def __lt__(self, other):
        return self.pages < other.pages
    
    # Arithmetic
    def __add__(self, other):
        return Book(
            f"{self.title} & {other.title}",
            f"{self.author} & {other.author}",
            self.pages + other.pages
        )
    
    # Container behavior
    def __len__(self):
        return self.pages
    
    def __getitem__(self, key):
        if key == "title":
            return self.title
        elif key == "author":
            return self.author
        raise KeyError(key)

book1 = Book("Python Guide", "Author A", 300)
book2 = Book("Java Guide", "Author B", 250)

print(book1)              # Uses __str__
print(book1 == book2)     # Uses __eq__
print(book1 < book2)      # Uses __lt__
print(len(book1))         # Uses __len__
print(book1["title"])     # Uses __getitem__
```

**More Magic Methods:**
```python
__init__      # Constructor
__del__       # Destructor
__call__      # Make instance callable
__getattr__   # Attribute access
__setattr__   # Attribute assignment
__iter__      # Make iterable
__next__      # Iterator protocol
__enter__     # Context manager entry
__exit__      # Context manager exit
```

---

## Exception Handling

### Q26. How does exception handling work in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Exception Handling

**Answer:**

Python uses `try`, `except`, `else`, and `finally` blocks for exception handling.

**Basic Syntax:**
```python
try:
    # Code that might raise exception
    result = 10 / 0
except ZeroDivisionError:
    # Handle specific exception
    print("Cannot divide by zero")
except ValueError as e:
    # Handle another exception
    print(f"Value error: {e}")
except Exception as e:
    # Catch all exceptions
    print(f"Error: {e}")
else:
    # Executes if no exception
    print("No errors")
finally:
    # Always executes
    print("Cleanup code")
```

**Example:**
```python
def divide(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"
    except TypeError:
        return "Invalid input types"
    else:
        return result
    finally:
        print("Division operation completed")

print(divide(10, 2))   # 5.0
print(divide(10, 0))   # "Cannot divide by zero"
```

**Raising Exceptions:**
```python
def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age > 150:
        raise ValueError("Age seems unrealistic")
    return True

try:
    validate_age(-5)
except ValueError as e:
    print(e)  # "Age cannot be negative"
```

**Custom Exceptions:**
```python
class CustomError(Exception):
    """Custom exception class."""
    pass

class ValidationError(Exception):
    def __init__(self, message, field):
        self.message = message
        self.field = field
        super().__init__(f"{field}: {message}")

try:
    raise ValidationError("Invalid value", "email")
except ValidationError as e:
    print(e.field)     # "email"
    print(e.message)   # "Invalid value"
```

---

### Q27. What is the difference between `raise`, `assert`, and `try-except`? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Exception Handling

**Answer:**

**1. `raise` - Explicitly raise exception:**
```python
def process_age(age):
    if age < 0:
        raise ValueError("Age must be positive")
    return age * 2
```

**2. `assert` - Debugging tool (can be disabled):**
```python
def divide(a, b):
    assert b != 0, "Divisor cannot be zero"
    return a / b

# Can be disabled with -O flag: python -O script.py
```

**3. `try-except` - Handle exceptions:**
```python
try:
    result = risky_operation()
except Exception as e:
    handle_error(e)
```

**When to Use:**

- **`raise`**: For expected error conditions that callers should handle
- **`assert`**: For debugging, internal consistency checks (can be disabled)
- **`try-except`**: For handling exceptions from code you call

**Best Practices:**
```python
# Good: Use raise for validation
def validate_input(value):
    if not value:
        raise ValueError("Value required")

# Good: Use assert for invariants
def process_data(data):
    assert data is not None, "Data cannot be None"
    # Process data

# Good: Use try-except for error handling
try:
    result = external_api_call()
except APIError as e:
    log_error(e)
    return default_value
```

---

## File I/O Operations

### Q28. How do you read and write files in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, I/O Operations, File Handling

**Answer:**

**Reading Files:**
```python
# Method 1: Using with statement (recommended)
with open("file.txt", "r") as file:
    content = file.read()  # Read entire file
    print(content)

# Method 2: Read line by line
with open("file.txt", "r") as file:
    for line in file:
        print(line.strip())

# Method 3: Read all lines
with open("file.txt", "r") as file:
    lines = file.readlines()  # List of lines

# Method 4: Read specific number of bytes
with open("file.txt", "r") as file:
    chunk = file.read(100)  # First 100 characters
```

**Writing Files:**
```python
# Write (overwrites existing)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("Second line\n")

# Append
with open("output.txt", "a") as file:
    file.write("Appended line\n")

# Write multiple lines
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("output.txt", "w") as file:
    file.writelines(lines)
```

**File Modes:**
```python
"r"   # Read (default for text)
"w"   # Write (overwrites)
"a"   # Append
"x"   # Exclusive creation (fails if exists)
"r+"  # Read and write
"b"   # Binary mode: "rb", "wb", "ab"
"t"   # Text mode (default)
```

**Binary Files:**
```python
# Read binary
with open("image.jpg", "rb") as file:
    data = file.read()

# Write binary
with open("copy.jpg", "wb") as file:
    file.write(data)
```

**Best Practices:**
- Always use `with` statement (automatic file closing)
- Handle exceptions
- Use appropriate mode
- Close files explicitly if not using `with`

---

### Q29. What are context managers? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Context Managers, Resource Management

**Answer:**

Context managers ensure proper setup and teardown of resources using `with` statement.

**Built-in Context Managers:**
```python
# File handling
with open("file.txt", "r") as file:
    content = file.read()
# File automatically closed

# Locks
import threading
lock = threading.Lock()
with lock:
    # Critical section
    pass
# Lock automatically released
```

**Custom Context Manager (Class-based):**
```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
        return False  # Don't suppress exceptions

# Usage
with FileManager("file.txt", "r") as file:
    content = file.read()
```

**Context Manager (Function-based):**
```python
from contextlib import contextmanager

@contextmanager
def file_manager(filename, mode):
    file = open(filename, mode)
    try:
        yield file
    finally:
        file.close()

# Usage
with file_manager("file.txt", "r") as file:
    content = file.read()
```

**Use Cases:**
- File operations
- Database connections
- Locks and synchronization
- Temporary changes (e.g., directory, environment)
- Resource cleanup

---

## Modules and Packages

### Q30. What is the difference between a module and a package? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Modules, Packages

**Answer:**

**Module:** A single Python file containing functions, classes, and variables.

```python
# math_utils.py (module)
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

# Usage
import math_utils
result = math_utils.add(2, 3)
```

**Package:** A directory containing multiple modules and an `__init__.py` file.

```
mypackage/
    __init__.py
    module1.py
    module2.py
    subpackage/
        __init__.py
        module3.py
```

```python
# mypackage/__init__.py
from .module1 import function1
from .module2 import function2

# Usage
import mypackage
from mypackage import function1
from mypackage.subpackage import module3
```

**Key Differences:**

| Feature | Module | Package |
|---------|--------|---------|
| **Structure** | Single `.py` file | Directory with `__init__.py` |
| **Import** | `import module` | `import package` |
| **Purpose** | Organize related code | Organize related modules |

**Python 3.3+ Namespace Packages:**
- Packages without `__init__.py` (implicit namespace packages)
- Useful for plugin systems

---

### Q31. How do you import modules in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Modules, Import

**Answer:**

**Different Import Styles:**

```python
# 1. Import entire module
import math
result = math.sqrt(16)

# 2. Import specific items
from math import sqrt, pi
result = sqrt(16)

# 3. Import all (not recommended)
from math import *
result = sqrt(16)

# 4. Import with alias
import numpy as np
import pandas as pd

# 5. Import from package
from mypackage import module1
from mypackage.module1 import function1

# 6. Relative imports (within package)
from . import sibling_module
from .. import parent_module
from .sibling_module import function
```

**Import Order (PEP 8):**
```python
# 1. Standard library
import os
import sys

# 2. Third-party
import numpy
import pandas

# 3. Local application
from mypackage import mymodule
```

**Import Best Practices:**
- Use absolute imports when possible
- Avoid `from module import *`
- Use aliases for long module names
- Group imports (stdlib, third-party, local)
- One import per line

---

## Decorators

### Q32. What are decorators in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Decorators, Functions

**Answer:**

Decorators are functions that modify or extend the behavior of other functions without permanently modifying them.

**Basic Decorator:**
```python
def my_decorator(func):
    def wrapper():
        print("Before function")
        result = func()
        print("After function")
        return result
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# Output:
# Before function
# Hello!
# After function
```

**Decorator with Arguments:**
```python
def decorator_with_args(message):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print(message)
            return func(*args, **kwargs)
        return wrapper
    return decorator

@decorator_with_args("Function called")
def add(a, b):
    return a + b
```

**Common Use Cases:**

**1. Timing:**
```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
```

**2. Logging:**
```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with {args}, {kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper
```

**3. Caching:**
```python
from functools import lru_cache

@lru_cache(maxsize=128)
def expensive_function(n):
    # Expensive computation
    return sum(i**2 for i in range(n))
```

**Class-based Decorator:**
```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"{self.func.__name__} called {self.count} times")
        return self.func(*args, **kwargs)

@CountCalls
def greet(name):
    return f"Hello, {name}!"
```

---

## Generators and Iterators

### Q33. What are generators in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Generators, Iterators, Memory Management

**Answer:**

Generators are functions that return an iterator using `yield` instead of `return`. They generate values lazily (on-demand).

**Generator Function:**
```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

# Usage
for i in countdown(5):
    print(i)  # 5, 4, 3, 2, 1
```

**Generator Expression:**
```python
# Similar to list comprehension but lazy
squares = (x**2 for x in range(10))
print(next(squares))  # 0
print(next(squares))  # 1

# List comprehension (eager)
squares_list = [x**2 for x in range(10)]  # Creates list immediately
```

**Benefits:**
- Memory efficient (generates values on-demand)
- Lazy evaluation
- Can represent infinite sequences

**Example - Infinite Sequence:**
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci()
for _ in range(10):
    print(next(fib))  # 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
```

**Sending Values to Generator:**
```python
def accumulator():
    total = 0
    while True:
        value = yield total
        if value is None:
            break
        total += value

acc = accumulator()
next(acc)  # Initialize
print(acc.send(10))  # 10
print(acc.send(20))  # 30
print(acc.send(5))   # 35
```

---

### Q34. What is the difference between generators and iterators? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Generators, Iterators

**Answer:**

**Iterator:** An object that implements `__iter__()` and `__next__()` methods.

```python
class CountIterator:
    def __init__(self, max_count):
        self.max_count = max_count
        self.current = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current < self.max_count:
            self.current += 1
            return self.current - 1
        raise StopIteration

# Usage
for i in CountIterator(5):
    print(i)  # 0, 1, 2, 3, 4
```

**Generator:** A function that uses `yield` (simpler way to create iterators).

```python
def count_generator(max_count):
    current = 0
    while current < max_count:
        yield current
        current += 1

# Usage
for i in count_generator(5):
    print(i)  # 0, 1, 2, 3, 4
```

**Key Differences:**

| Feature | Iterator | Generator |
|---------|----------|-----------|
| **Definition** | Class with `__iter__` and `__next__` | Function with `yield` |
| **Code** | More verbose | More concise |
| **State** | Manual state management | Automatic |
| **Memory** | Can be memory efficient | Memory efficient |
| **Use Case** | Complex iteration logic | Simple iteration |

**All generators are iterators, but not all iterators are generators.**

---

## Comprehensions

### Q35. What are list, dictionary, and set comprehensions? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Comprehensions, Data Structures

**Answer:**

Comprehensions provide a concise way to create lists, dictionaries, and sets.

**List Comprehension:**
```python
# Traditional
squares = []
for x in range(10):
    squares.append(x**2)

# List comprehension
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# With condition
evens = [x for x in range(10) if x % 2 == 0]
# [0, 2, 4, 6, 8]

# Nested
matrix = [[i*j for j in range(3)] for i in range(3)]
# [[0, 0, 0], [0, 1, 2], [0, 2, 4]]
```

**Dictionary Comprehension:**
```python
# Traditional
squares_dict = {}
for x in range(5):
    squares_dict[x] = x**2

# Dictionary comprehension
squares_dict = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# With condition
evens_dict = {x: x**2 for x in range(10) if x % 2 == 0}
# {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# From two lists
keys = ['a', 'b', 'c']
values = [1, 2, 3]
mapping = {k: v for k, v in zip(keys, values)}
# {'a': 1, 'b': 2, 'c': 3}
```

**Set Comprehension:**
```python
# Traditional
unique_squares = set()
for x in range(10):
    unique_squares.add(x**2)

# Set comprehension
unique_squares = {x**2 for x in range(10)}
# {0, 1, 64, 4, 36, 9, 16, 49, 25, 81}

# With condition
unique_evens = {x**2 for x in range(10) if x % 2 == 0}
# {0, 16, 4, 64, 36}
```

**Generator Expression:**
```python
# Similar to list comprehension but lazy
squares_gen = (x**2 for x in range(10))
print(list(squares_gen))  # Convert to list if needed
```

**Benefits:**
- More concise and readable
- Often faster than loops
- Pythonic way to create collections

---

## Regular Expressions

### Q36. How do you use regular expressions in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Regular Expressions, String Operations

**Answer:**

Python's `re` module provides regular expression operations.

**Basic Usage:**
```python
import re

# Search
text = "The price is $100"
match = re.search(r'\$(\d+)', text)
if match:
    print(match.group(1))  # "100"

# Match (from start)
result = re.match(r'Hello', "Hello World")  # Match
result = re.match(r'World', "Hello World")  # None

# Find all
text = "Contact: alice@example.com, bob@test.com"
emails = re.findall(r'\b[\w.-]+@[\w.-]+\.\w+\b', text)
# ['alice@example.com', 'bob@test.com']

# Split
text = "apple,banana,cherry"
items = re.split(r',', text)
# ['apple', 'banana', 'cherry']

# Substitute
text = "Hello World"
new_text = re.sub(r'World', 'Python', text)
# "Hello Python"
```

**Common Patterns:**
```python
# Email
email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'

# Phone number
phone_pattern = r'\d{3}-\d{3}-\d{4}'

# URL
url_pattern = r'https?://(?:[-\w.])+(?:[:\d]+)?(?:/(?:[\w/_.])*(?:\?(?:[\w&=%.])*)?(?:#(?:\w*))?)?'

# Digits
digits = re.findall(r'\d+', "I have 5 apples and 10 oranges")
# ['5', '10']
```

**Compiled Patterns:**
```python
# Compile for reuse
pattern = re.compile(r'\d+')
matches = pattern.findall("I have 5 apples")
# ['5']

# More efficient for repeated use
```

**Groups:**
```python
text = "Date: 2024-01-15"
match = re.search(r'(\d{4})-(\d{2})-(\d{2})', text)
if match:
    year = match.group(1)   # "2024"
    month = match.group(2)  # "01"
    day = match.group(3)    # "15"
    full_date = match.group(0)  # "2024-01-15"
```

---

## Database Operations

### Q37. How do you connect to a database in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Backend, Database, SQL

**Answer:**

**SQLite (Built-in):**
```python
import sqlite3

# Connect
conn = sqlite3.connect('database.db')
cursor = conn.cursor()

# Create table
cursor.execute('''
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        email TEXT UNIQUE
    )
''')

# Insert
cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", 
               ("Alice", "alice@example.com"))
conn.commit()

# Query
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()
for row in rows:
    print(row)

# Close
conn.close()

# Using context manager
with sqlite3.connect('database.db') as conn:
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM users")
    rows = cursor.fetchall()
```

**PostgreSQL (psycopg2):**
```python
import psycopg2

conn = psycopg2.connect(
    host="localhost",
    database="mydb",
    user="user",
    password="password"
)

cursor = conn.cursor()
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()
conn.close()
```

**MySQL (mysql-connector-python):**
```python
import mysql.connector

conn = mysql.connector.connect(
    host="localhost",
    database="mydb",
    user="user",
    password="password"
)

cursor = conn.cursor()
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()
conn.close()
```

**Using ORM (SQLAlchemy):**
```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    email = Column(String(100))

engine = create_engine('sqlite:///database.db')
Base.metadata.create_all(engine)

Session = sessionmaker(bind=engine)
session = Session()

# Create
user = User(name="Alice", email="alice@example.com")
session.add(user)
session.commit()

# Query
users = session.query(User).all()
```

---

## Web Development

### Q38. How do you create a web server in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Backend, Web, HTTP, API

**Answer:**

**Flask:**
```python
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, World!"

@app.route('/api/users', methods=['GET'])
def get_users():
    users = [{"id": 1, "name": "Alice"}]
    return jsonify(users)

@app.route('/api/users', methods=['POST'])
def create_user():
    data = request.json
    # Process data
    return jsonify({"id": 1, "name": data["name"]}), 201

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

**Django:**
```python
# views.py
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
import json

@csrf_exempt
def users(request):
    if request.method == 'GET':
        users = [{"id": 1, "name": "Alice"}]
        return JsonResponse(users, safe=False)
    elif request.method == 'POST':
        data = json.loads(request.body)
        return JsonResponse({"id": 1, "name": data["name"]}, status=201)
```

**FastAPI:**
```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    name: str
    email: str

@app.get("/")
def home():
    return {"message": "Hello, World!"}

@app.get("/api/users")
def get_users():
    return [{"id": 1, "name": "Alice"}]

@app.post("/api/users")
def create_user(user: User):
    return {"id": 1, "name": user.name, "email": user.email}
```

---

### Q39. What is the difference between Flask, Django, and FastAPI? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Backend, Web, Framework Comparison

**Answer:**

| Feature | Flask | Django | FastAPI |
|---------|-------|--------|---------|
| **Type** | Microframework | Full-stack framework | Modern async framework |
| **Complexity** | Simple, minimal | Complex, feature-rich | Moderate |
| **Use Case** | Small to medium apps | Large applications | APIs, microservices |
| **ORM** | External (SQLAlchemy) | Built-in (Django ORM) | External (SQLAlchemy) |
| **Admin Panel** | External | Built-in | External |
| **Async Support** | Limited | Limited (3.0+) | Native |
| **Performance** | Good | Good | Excellent (async) |
| **Learning Curve** | Easy | Steep | Moderate |
| **Best For** | APIs, prototypes | Web apps, CMS | High-performance APIs |

**When to Use:**

- **Flask:** Simple APIs, microservices, learning
- **Django:** Full web applications, CMS, admin needed
- **FastAPI:** High-performance APIs, async operations, automatic docs

---

## Testing

### Q40. How do you write tests in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Testing, Quality Assurance

**Answer:**

**unittest (Built-in):**
```python
import unittest

class TestMath(unittest.TestCase):
    def setUp(self):
        # Setup before each test
        self.numbers = [1, 2, 3, 4, 5]
    
    def test_sum(self):
        self.assertEqual(sum(self.numbers), 15)
    
    def test_max(self):
        self.assertEqual(max(self.numbers), 5)
    
    def tearDown(self):
        # Cleanup after each test
        pass

if __name__ == '__main__':
    unittest.main()
```

**pytest (Popular):**
```python
# test_math.py
def test_sum():
    assert sum([1, 2, 3]) == 6

def test_max():
    assert max([1, 2, 3]) == 3

# Fixtures
import pytest

@pytest.fixture
def sample_data():
    return [1, 2, 3, 4, 5]

def test_sum_with_fixture(sample_data):
    assert sum(sample_data) == 15
```

**Running Tests:**
```bash
# unittest
python -m unittest test_math.py

# pytest
pytest test_math.py
pytest -v  # Verbose
pytest -k test_sum  # Run specific test
```

---

## Async/Await

### Q41. What is async/await in Python? (Medium)

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Async, Concurrency, Backend

**Answer:**

`async/await` enables asynchronous programming for concurrent I/O operations.

**Basic Syntax:**
```python
import asyncio

async def fetch_data():
    await asyncio.sleep(1)  # Simulate I/O
    return "Data"

async def main():
    result = await fetch_data()
    print(result)

asyncio.run(main())
```

**Multiple Concurrent Operations:**
```python
import asyncio
import aiohttp

async def fetch_url(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main():
    async with aiohttp.ClientSession() as session:
        urls = ["http://example.com", "http://example.org"]
        tasks = [fetch_url(session, url) for url in urls]
        results = await asyncio.gather(*tasks)
        return results

asyncio.run(main())
```

**Use Cases:**
- I/O-bound operations (network requests, file I/O)
- Web scraping
- API calls
- Database operations

**Benefits:**
- Non-blocking I/O
- Better resource utilization
- Scalable for many concurrent operations

---

## Memory Management

### Q42. How does Python manage memory? (Tough)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Memory Management, Performance

**Answer:**

Python uses automatic memory management with reference counting and garbage collection.

**Reference Counting:**
- Each object has a reference count
- Count increases when referenced
- Count decreases when dereferenced
- Object deleted when count reaches 0

**Garbage Collection:**
- Cyclic reference detector
- Detects and collects circular references
- Runs automatically (can be controlled)

**Example:**
```python
import sys

x = [1, 2, 3]
print(sys.getrefcount(x))  # Reference count

# Circular reference
a = []
b = []
a.append(b)
b.append(a)
# Reference counting can't free these
# Garbage collector handles it
```

**Memory Management Tools:**
```python
import gc

# Force garbage collection
gc.collect()

# Get statistics
stats = gc.get_stats()
```

---

## Advanced Topics

### Q43. What is the Global Interpreter Lock (GIL)? (Tough)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Concurrency, Performance, GIL

**Answer:**

The GIL is a mutex that allows only one thread to execute Python bytecode at a time.

**Implications:**
- Prevents true parallel execution of Python code
- I/O-bound operations can still benefit from threading
- CPU-bound operations don't benefit from threading
- Use multiprocessing for CPU-bound tasks

**Workarounds:**
```python
# Multiprocessing (bypasses GIL)
from multiprocessing import Process

def cpu_bound_task():
    # CPU-intensive work
    pass

if __name__ == '__main__':
    processes = [Process(target=cpu_bound_task) for _ in range(4)]
    for p in processes:
        p.start()
    for p in processes:
        p.join()
```

**When GIL Doesn't Matter:**
- I/O-bound operations (network, file I/O)
- C extensions that release GIL
- Async/await (single-threaded)

---

### Q44. What are metaclasses? (Tough)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, OOP, Metaclasses, Advanced

**Answer:**

Metaclasses are classes of classes. They define how classes are created.

**Basic Metaclass:**
```python
class MyMeta(type):
    def __new__(cls, name, bases, dct):
        # Customize class creation
        dct['custom_attr'] = 'Added by metaclass'
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=MyMeta):
    pass

print(MyClass.custom_attr)  # "Added by metaclass"
```

**Use Cases:**
- Framework development
- API design
- Automatic registration
- Validation

**Note:** Metaclasses are advanced and rarely needed in everyday programming.

---

### Q45. What are virtual environments and why are they important? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Environment, Package Management

**Answer:**

Virtual environments isolate Python packages for different projects.

**Creating Virtual Environment:**
```bash
# Using venv (Python 3.3+)
python -m venv myenv

# Activate (Windows)
myenv\Scripts\activate

# Activate (Linux/Mac)
source myenv/bin/activate

# Deactivate
deactivate
```

**Using virtualenv:**
```bash
pip install virtualenv
virtualenv myenv
source myenv/bin/activate
```

**Benefits:**
- Isolate project dependencies
- Avoid version conflicts
- Reproducible environments
- Easy deployment

**requirements.txt:**
```bash
# Generate
pip freeze > requirements.txt

# Install
pip install -r requirements.txt
```

---

### Q46. What are type hints in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Type Hints, Code Quality

**Answer:**

Type hints (PEP 484) add type information to function signatures and variables.

**Basic Usage:**
```python
from typing import List, Dict, Optional, Union

def greet(name: str) -> str:
    return f"Hello, {name}"

def process_numbers(numbers: List[int]) -> int:
    return sum(numbers)

def get_user(id: int) -> Optional[Dict[str, str]]:
    if id > 0:
        return {"id": str(id), "name": "Alice"}
    return None

def process(value: Union[int, str]) -> str:
    return str(value)
```

**Type Aliases:**
```python
from typing import List, Tuple

Point = Tuple[float, float]
Coordinates = List[Point]

def draw(points: Coordinates) -> None:
    pass
```

**Generic Types:**
```python
from typing import TypeVar, Generic

T = TypeVar('T')

class Stack(Generic[T]):
    def __init__(self):
        self.items: List[T] = []
    
    def push(self, item: T) -> None:
        self.items.append(item)
    
    def pop(self) -> T:
        return self.items.pop()
```

**Benefits:**
- Better IDE support
- Type checking with mypy
- Self-documenting code
- Catch errors early

---

### Q47. What are data classes? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Data Classes

**Answer:**

Data classes (Python 3.7+) automatically generate special methods for classes.

**Basic Data Class:**
```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int
    email: str = ""  # Default value

# Automatically generates:
# __init__, __repr__, __eq__, etc.

person = Person("Alice", 30, "alice@example.com")
print(person)  # Person(name='Alice', age=30, email='alice@example.com')
```

**Advanced Features:**
```python
from dataclasses import dataclass, field

@dataclass
class Point:
    x: float
    y: float
    
    def distance(self) -> float:
        return (self.x**2 + self.y**2)**0.5

@dataclass
class Inventory:
    items: list = field(default_factory=list)
    total: int = 0
```

**Frozen Data Class (Immutable):**
```python
@dataclass(frozen=True)
class Point:
    x: float
    y: float

p = Point(1, 2)
# p.x = 3  # Error! Frozen
```

**Benefits:**
- Less boilerplate code
- Automatic method generation
- Type hints support
- Cleaner syntax

---

### Q48. How do you work with JSON in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, JSON, I/O Operations, Backend

**Answer:**

Python's `json` module handles JSON encoding and decoding.

**Basic Usage:**
```python
import json

# Python to JSON (serialize)
data = {
    "name": "Alice",
    "age": 30,
    "city": "NYC"
}
json_string = json.dumps(data)
# '{"name": "Alice", "age": 30, "city": "NYC"}'

# JSON to Python (deserialize)
data = json.loads(json_string)
# {'name': 'Alice', 'age': 30, 'city': 'NYC'}

# Pretty print
json_string = json.dumps(data, indent=2)

# File operations
with open("data.json", "w") as f:
    json.dump(data, f)

with open("data.json", "r") as f:
    data = json.load(f)
```

**Custom Encoding:**
```python
import json
from datetime import datetime

class DateTimeEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, datetime):
            return obj.isoformat()
        return super().default(obj)

data = {"timestamp": datetime.now()}
json_string = json.dumps(data, cls=DateTimeEncoder)
```

---

### Q49. How do you work with CSV files? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, CSV, I/O Operations, Data Processing

**Answer:**

Python's `csv` module handles CSV file operations.

**Reading CSV:**
```python
import csv

# Method 1: csv.reader
with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Method 2: csv.DictReader (with headers)
with open("data.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["name"], row["age"])

# Method 3: pandas
import pandas as pd
df = pd.read_csv("data.csv")
```

**Writing CSV:**
```python
import csv

# Method 1: csv.writer
data = [["Name", "Age"], ["Alice", 30], ["Bob", 25]]
with open("output.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(data)

# Method 2: csv.DictWriter
fieldnames = ["name", "age"]
data = [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]
with open("output.csv", "w", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(data)
```

---

### Q50. What is the collections module? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Collections, Data Structures

**Answer:**

The `collections` module provides specialized container datatypes.

**1. Counter:**
```python
from collections import Counter

# Count occurrences
counter = Counter([1, 2, 2, 3, 3, 3])
print(counter)  # Counter({3: 3, 2: 2, 1: 1})

# Most common
counter.most_common(2)  # [(3, 3), (2, 2)]
```

**2. defaultdict:**
```python
from collections import defaultdict

# Default value for missing keys
dd = defaultdict(list)
dd["fruits"].append("apple")
dd["fruits"].append("banana")
# No KeyError for missing keys
```

**3. OrderedDict:**
```python
from collections import OrderedDict

# Maintains insertion order (Python 3.7+ dicts do this too)
od = OrderedDict()
od["first"] = 1
od["second"] = 2
```

**4. deque:**
```python
from collections import deque

# Double-ended queue
dq = deque([1, 2, 3])
dq.appendleft(0)  # Add to left
dq.popleft()      # Remove from left
dq.append(4)      # Add to right
dq.pop()          # Remove from right
```

**5. namedtuple:**
```python
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])
p = Point(1, 2)
print(p.x, p.y)  # 1 2
```

---

### Q51. What is the itertools module? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Itertools, Iterators

**Answer:**

The `itertools` module provides iterator building blocks.

**Common Functions:**
```python
import itertools

# Infinite iterators
counter = itertools.count(1, 2)  # 1, 3, 5, 7, ...
cycle = itertools.cycle([1, 2, 3])  # 1, 2, 3, 1, 2, 3, ...
repeat = itertools.repeat(10, 3)  # 10, 10, 10

# Combinatoric iterators
combinations = itertools.combinations([1, 2, 3], 2)
# (1, 2), (1, 3), (2, 3)

permutations = itertools.permutations([1, 2, 3], 2)
# All permutations

product = itertools.product([1, 2], [3, 4])
# (1, 3), (1, 4), (2, 3), (2, 4)

# Iterators
chain = itertools.chain([1, 2], [3, 4])  # 1, 2, 3, 4
groupby = itertools.groupby([1, 1, 2, 2, 3])
# Groups consecutive identical elements
```

---

### Q52. How do you work with dates and times? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, DateTime, I/O Operations

**Answer:**

Python's `datetime` module handles dates and times.

**Basic Usage:**
```python
from datetime import datetime, date, time, timedelta

# Current date/time
now = datetime.now()
today = date.today()

# Create specific date/time
dt = datetime(2024, 1, 15, 10, 30, 0)
d = date(2024, 1, 15)
t = time(10, 30, 0)

# Formatting
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
# "2024-01-15 10:30:00"

# Parsing
dt = datetime.strptime("2024-01-15", "%Y-%m-%d")

# Arithmetic
future = now + timedelta(days=7)
past = now - timedelta(hours=2)
difference = future - now
```

**Timezone:**
```python
from datetime import datetime, timezone, timedelta

# UTC
utc_now = datetime.now(timezone.utc)

# Timezone-aware
tz = timezone(timedelta(hours=5, minutes=30))
dt = datetime.now(tz)
```

---

### Q53. How do you handle environment variables? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Environment Variables, Configuration, Backend

**Answer:**

**Using os module:**
```python
import os

# Get environment variable
api_key = os.getenv("API_KEY")
api_key = os.getenv("API_KEY", "default_value")  # With default

# Check if exists
if "API_KEY" in os.environ:
    api_key = os.environ["API_KEY"]

# Set (for current process)
os.environ["API_KEY"] = "new_value"
```

**Using python-dotenv:**
```python
from dotenv import load_dotenv
import os

# Load from .env file
load_dotenv()

api_key = os.getenv("API_KEY")
```

**.env file:**
```
API_KEY=secret_key_123
DATABASE_URL=postgresql://localhost/db
DEBUG=True
```

**Best Practices:**
- Never commit `.env` files
- Use environment variables for secrets
- Provide defaults for development
- Validate required variables

---

### Q54. What are some common security practices in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer, Senior Developer  
**Tags:** Backend, Security, Best Practices

**Answer:**

**1. Input Validation:**
```python
import re

def validate_email(email):
    pattern = r'^[\w.-]+@[\w.-]+\.\w+$'
    return bool(re.match(pattern, email))
```

**2. SQL Injection Prevention:**
```python
# Bad (vulnerable)
query = f"SELECT * FROM users WHERE id = {user_id}"

# Good (parameterized)
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))
```

**3. Password Hashing:**
```python
import hashlib
from werkzeug.security import generate_password_hash, check_password_hash

# Hash password
password_hash = generate_password_hash("password123")

# Verify
is_valid = check_password_hash(password_hash, "password123")
```

**4. Secure Random:**
```python
import secrets

# Generate secure token
token = secrets.token_urlsafe(32)

# Random choice
choice = secrets.choice(["option1", "option2"])
```

**5. HTTPS:**
```python
# Always use HTTPS in production
# Verify SSL certificates
import requests
response = requests.get("https://api.example.com", verify=True)
```

**6. Sanitize Input:**
```python
import html

# Escape HTML
safe_html = html.escape(user_input)
```

---

### Q55. How do you optimize Python code performance? (Medium)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Performance, Optimization

**Answer:**

**1. Use Built-in Functions:**
```python
# Slow
result = []
for item in items:
    result.append(item * 2)

# Fast
result = [item * 2 for item in items]
result = list(map(lambda x: x * 2, items))
```

**2. Avoid Global Lookups:**
```python
# Slow
def process():
    for i in range(1000):
        result = len(items)  # Global lookup

# Fast
def process():
    length = len(items)  # Local variable
    for i in range(1000):
        result = length
```

**3. Use Generators:**
```python
# Memory efficient
def read_large_file(filename):
    with open(filename) as f:
        for line in f:
            yield process(line)
```

**4. Use Appropriate Data Structures:**
```python
# Set for membership testing (O(1))
if item in my_set:  # Fast
    pass

# List for membership testing (O(n))
if item in my_list:  # Slow for large lists
    pass
```

**5. Profile Code:**
```python
import cProfile

def my_function():
    # Code to profile
    pass

cProfile.run('my_function()')
```

**6. Use C Extensions:**
- NumPy for numerical computations
- Cython for performance-critical code
- Use compiled languages for bottlenecks

---

### Q56. What is the difference between `__str__` and `__repr__`? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Magic Methods

**Answer:**

- `__str__`: User-friendly string representation
- `__repr__`: Developer-friendly, unambiguous representation

**Example:**
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"Point({self.x}, {self.y})"
    
    def __repr__(self):
        return f"Point(x={self.x}, y={self.y})"

p = Point(1, 2)
print(str(p))    # Point(1, 2) - uses __str__
print(repr(p))    # Point(x=1, y=2) - uses __repr__
```

**Best Practice:**
- `__repr__` should be unambiguous and ideally recreate the object
- `__str__` should be readable for end users
- If `__str__` is not defined, `__repr__` is used as fallback

---

### Q57. How do you implement singleton pattern in Python? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Design Patterns

**Answer:**

**Method 1: Decorator**
```python
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class Database:
    def __init__(self):
        print("Database initialized")

db1 = Database()  # Database initialized
db2 = Database()  # No output (reused)
print(db1 is db2)  # True
```

**Method 2: Metaclass**
```python
class SingletonMeta(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Database(metaclass=SingletonMeta):
    def __init__(self):
        print("Database initialized")
```

**Method 3: `__new__` method**
```python
class Singleton:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

---

### Q58. What is the difference between `append()` and `extend()`? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Data Structures, Lists

**Answer:**

- `append()`: Adds a single element to the end
- `extend()`: Adds all elements from an iterable

**Example:**
```python
lst = [1, 2, 3]

# append
lst.append(4)        # [1, 2, 3, 4]
lst.append([5, 6])   # [1, 2, 3, 4, [5, 6]]

# extend
lst = [1, 2, 3]
lst.extend([4, 5])   # [1, 2, 3, 4, 5]
lst.extend("abc")    # [1, 2, 3, 4, 5, 'a', 'b', 'c']
```

**Key Difference:**
- `append()` adds the object itself (can be nested)
- `extend()` adds elements from the iterable (flattens)

---

### Q59. How do you handle file paths in Python? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, I/O Operations, File Handling

**Answer:**

Use `pathlib` (Python 3.4+) for path operations.

**Basic Usage:**
```python
from pathlib import Path

# Create path
p = Path("folder/file.txt")
p = Path("/absolute/path/file.txt")

# Join paths
p = Path("folder") / "subfolder" / "file.txt"

# Get parts
p.name        # "file.txt"
p.stem        # "file"
p.suffix      # ".txt"
p.parent      # Path("folder/subfolder")

# Check existence
p.exists()    # True/False
p.is_file()   # True/False
p.is_dir()    # True/False

# Operations
p.mkdir(parents=True, exist_ok=True)  # Create directory
p.unlink()    # Delete file
p.rename("new_name.txt")  # Rename

# Read/Write
content = p.read_text()
p.write_text("Hello, World!")

# Iterate directory
for file in Path(".").iterdir():
    print(file)
```

**Legacy (os.path):**
```python
import os

path = os.path.join("folder", "file.txt")
exists = os.path.exists(path)
is_file = os.path.isfile(path)
```

---

### Q60. What is the difference between `deepcopy` and `copy`? (Medium)

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, OOP, Memory Management

**Answer:**

- `copy.copy()`: Shallow copy (copies object, but nested objects are referenced)
- `copy.deepcopy()`: Deep copy (recursively copies all nested objects)

**Example:**
```python
import copy

original = [[1, 2, 3], [4, 5, 6]]

# Shallow copy
shallow = copy.copy(original)
shallow[0][0] = 'X'
print(original)  # [['X', 2, 3], [4, 5, 6]] (changed!)

# Deep copy
deep = copy.deepcopy(original)
deep[0][0] = 'Y'
print(original)  # [['X', 2, 3], [4, 5, 6]] (unchanged)
```

**When to Use:**
- Shallow copy: When nested objects don't need to be independent
- Deep copy: When you need completely independent copies

---

## Summary

This comprehensive guide covers Python interview topics from basics to advanced concepts:

- **Basics:** Variables, data types, operators, control flow
- **Functions:** Definition, arguments, lambda, closures
- **Data Structures:** Lists, tuples, sets, dictionaries
- **OOP:** Classes, inheritance, polymorphism, encapsulation
- **Advanced:** Decorators, generators, async/await
- **Backend:** Web frameworks, databases, APIs
- **Testing:** unittest, pytest
- **Memory:** GIL, garbage collection

**Difficulty Levels:**
- **Basic:** Fundamentals, syntax, simple operations
- **Intermediate:** Common patterns, OOP, standard library
- **Advanced:** Metaclasses, GIL, performance optimization

**Role Suitability:**
- **Junior Developer:** Basic to intermediate topics
- **Intermediate Developer:** Most topics except advanced
- **Senior Developer/Architect:** All topics including advanced

---

## References

- [Python Roadmap](https://roadmap.sh/python)
- [Official Python Documentation](https://docs.python.org/)
- [PEP 8 Style Guide](https://pep8.org/)
- [Real Python](https://realpython.com/)

---

*Last Updated: 2024*

