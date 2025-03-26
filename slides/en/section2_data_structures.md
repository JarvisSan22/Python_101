# Section 2: Data Structures

## Lists, Tuples, Sets and Dictionaries

### Lists
- Ordered, mutable collections of items
- Created with square brackets `[]`
- Can contain items of different types
- Zero-indexed (first element is at index 0)

```python
# Creating a list
japanese_fish = ["Koi", "Fugu", "Tai", "Maguro", "Unagi"]

# Accessing elements
first_fish = japanese_fish[0]  # "Koi"
last_fish = japanese_fish[-1]  # "Unagi"

# Slicing
first_three = japanese_fish[0:3]  # ["Koi", "Fugu", "Tai"]
last_two = japanese_fish[-2:]  # ["Maguro", "Unagi"]

# Modifying lists
japanese_fish[1] = "Hirame"  # Replace "Fugu" with "Hirame"
japanese_fish.append("Saba")  # Add "Saba" to the end
japanese_fish.insert(2, "Aji")  # Insert "Aji" at index 2
removed_fish = japanese_fish.pop()  # Remove and return the last item
japanese_fish.remove("Tai")  # Remove "Tai" from the list

# List operations
fish_count = len(japanese_fish)  # Number of items in the list
is_present = "Koi" in japanese_fish  # Check if "Koi" is in the list
```

### Common List Methods
- `append()`: Add an item to the end
- `insert()`: Insert an item at a specific position
- `remove()`: Remove a specific item
- `pop()`: Remove and return an item at a specific position
- `index()`: Find the position of an item
- `count()`: Count occurrences of an item
- `sort()`: Sort the list in-place
- `reverse()`: Reverse the list in-place
- `copy()`: Create a shallow copy of the list

### List Comprehensions
- Concise way to create lists
- Based on existing lists or other iterables

```python
# Traditional way
squares = []
for i in range(1, 6):
    squares.append(i ** 2)
print(squares)  # [1, 4, 9, 16, 25]

# Using list comprehension
squares = [i ** 2 for i in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# List comprehension with condition
even_squares = [i ** 2 for i in range(1, 11) if i % 2 == 0]
print(even_squares)  # [4, 16, 36, 64, 100]
```

---

### Tuples
- Ordered, immutable collections of items
- Created with parentheses `()`
- Similar to lists, but cannot be modified after creation
- Used for data that shouldn't change

```python
# Creating a tuple
fish_info = ("Koi", 3, 2.5, "Freshwater")

# Accessing elements
fish_name = fish_info[0]  # "Koi"
fish_age = fish_info[1]  # 3

# Tuple unpacking
name, age, weight, habitat = fish_info

# Single-item tuple (note the comma)
single_fish = ("Fugu",)  # Without the comma, it would be a string in parentheses

# Tuple operations
length = len(fish_info)  # 4
is_present = "Koi" in fish_info  # True
```

### When to Use Tuples vs Lists
- Use tuples for:
  - Immutable data (that shouldn't change)
  - Faster access than lists
  - Dictionary keys (lists cannot be used as keys)
  - Function return values with multiple items
- Use lists for:
  - Collections that need to be modified
  - When you need to add or remove items
  - When order matters and may change

---

### Sets
- Unordered collections of unique items
- Created with curly braces `{}` or the `set()` constructor
- No duplicate elements
- Fast membership testing
- Mathematical set operations (union, intersection, etc.)

```python
# Creating a set
freshwater_fish = {"Koi", "Goldfish", "Unagi", "Koi"}  # Note: duplicates are removed
print(freshwater_fish)  # {'Koi', 'Goldfish', 'Unagi'}

# Creating a set from a list
saltwater_fish = set(["Tai", "Maguro", "Hirame", "Tai"])
print(saltwater_fish)  # {'Tai', 'Maguro', 'Hirame'}

# Set operations
all_fish = freshwater_fish.union(saltwater_fish)  # All fish from both sets
common_fish = freshwater_fish.intersection(saltwater_fish)  # Fish in both sets
unique_to_freshwater = freshwater_fish.difference(saltwater_fish)  # Fish only in freshwater
```

### Common Set Methods
- `add()`: Add an element
- `remove()`: Remove an element (raises error if not present)
- `discard()`: Remove an element if present
- `pop()`: Remove and return an arbitrary element
- `clear()`: Remove all elements
- `union()`: Return a set with elements from both sets
- `intersection()`: Return a set with elements common to both sets
- `difference()`: Return a set with elements in the first set but not the second
- `symmetric_difference()`: Return a set with elements in either set, but not both

---

### Dictionaries
- Unordered collections of key-value pairs
- Created with curly braces `{}` and colons `:`
- Keys must be immutable (strings, numbers, tuples)
- Values can be any type
- Fast lookup by key

```python
# Creating a dictionary
fish_details = {
    "name": "Koi",
    "age": 3,
    "weight": 2.5,
    "colors": ["red", "white", "black"],
    "is_freshwater": True
}

# Accessing values
name = fish_details["name"]  # "Koi"
age = fish_details.get("age")  # 3
# Using get() with a default value
price = fish_details.get("price", "Not for sale")  # "Not for sale"

# Modifying dictionaries
fish_details["weight"] = 2.7  # Update value
fish_details["price"] = 5000  # Add new key-value pair
del fish_details["age"]  # Remove a key-value pair
```

### Dictionary Methods
- `keys()`: Return a view of all keys
- `values()`: Return a view of all values
- `items()`: Return a view of all key-value pairs
- `get()`: Return the value for a key, with an optional default
- `pop()`: Remove and return the value for a key
- `update()`: Update with key-value pairs from another dictionary
- `clear()`: Remove all items

### Dictionary Comprehensions
- Similar to list comprehensions, but create dictionaries

```python
# Creating a dictionary with comprehension
fish_lengths = {fish: len(fish) for fish in ["Koi", "Fugu", "Tai", "Maguro"]}
print(fish_lengths)  # {'Koi': 3, 'Fugu': 4, 'Tai': 3, 'Maguro': 6}
```

---

## String Operations and Formatting

### String Basics
- Strings are sequences of characters
- Immutable (cannot be changed after creation)
- Created with single quotes `'`, double quotes `"`, or triple quotes `'''` or `"""`
- Indexed like lists (zero-based)

```python
# String creation
fish_name = "Koi"
description = 'Japanese ornamental fish'
info = """Koi are colored varieties of the
Amur carp that are kept for decorative
purposes in outdoor ponds or water gardens."""
```

### String Indexing and Slicing
```python
fish = "Maguro"

# Indexing
first_char = fish[0]  # 'M'
last_char = fish[-1]  # 'o'

# Slicing
first_three = fish[0:3]  # 'Mag'
last_three = fish[-3:]  # 'uro'
```

### String Methods
- `upper()`, `lower()`, `title()`: Change case
- `strip()`, `lstrip()`, `rstrip()`: Remove whitespace
- `replace()`: Replace substrings
- `split()`: Split into a list
- `join()`: Join a list into a string
- `find()`, `index()`: Find substrings
- `startswith()`, `endswith()`: Check prefix/suffix
- `isalpha()`, `isdigit()`, `isalnum()`: Check content type

```python
fish = "  Maguro Tuna  "

# Case methods
print(fish.upper())  # "  MAGURO TUNA  "
print(fish.lower())  # "  maguro tuna  "
print(fish.title())  # "  Maguro Tuna  "

# Whitespace removal
print(fish.strip())  # "Maguro Tuna"
print(fish.lstrip())  # "Maguro Tuna  "
print(fish.rstrip())  # "  Maguro Tuna"

# Replacement
print(fish.replace("Tuna", "Sashimi"))  # "  Maguro Sashimi  "

# Splitting
words = fish.strip().split()
print(words)  # ["Maguro", "Tuna"]

# Joining
fish_list = ["Koi", "Fugu", "Tai"]
joined = ", ".join(fish_list)
print(joined)  # "Koi, Fugu, Tai"

# Finding
position = "Japanese Koi Fish".find("Koi")
print(position)  # 9

# Checking
print("Koi".isalpha())  # True
print("123".isdigit())  # True
print("Koi123".isalnum())  # True
```

### String Formatting

#### %-formatting (older style)
```python
name = "Koi"
age = 3
weight = 2.5

print("Fish: %s, Age: %d, Weight: %.1f kg" % (name, age, weight))
# "Fish: Koi, Age: 3, Weight: 2.5 kg"
```

#### str.format() method
```python
print("Fish: {}, Age: {}, Weight: {:.1f} kg".format(name, age, weight))
# "Fish: Koi, Age: 3, Weight: 2.5 kg"

# With positional arguments
print("Fish: {0}, Age: {1}, Weight: {2:.1f} kg".format(name, age, weight))

# With named arguments
print("Fish: {n}, Age: {a}, Weight: {w:.1f} kg".format(n=name, a=age, w=weight))
```

#### f-strings (Python 3.6+, recommended)
```python
print(f"Fish: {name}, Age: {age}, Weight: {weight:.1f} kg")
# "Fish: Koi, Age: 3, Weight: 2.5 kg"

# With expressions
print(f"Fish: {name.upper()}, Age in months: {age * 12}")
```

### Raw Strings
- Prefixed with `r`
- Backslashes are treated as literal characters
- Useful for regular expressions and file paths

```python
# Normal string
path = "C:\\Users\\Username\\Documents"
print(path)  # C:\Users\Username\Documents

# Raw string
path = r"C:\Users\Username\Documents"
print(path)  # C:\Users\Username\Documents
```

### String Concatenation
```python
# Using + operator
full_name = "Koi" + " " + "Fish"
print(full_name)  # "Koi Fish"

# Using join() method (more efficient for multiple strings)
parts = ["Japanese", "Ornamental", "Koi", "Fish"]
full_description = " ".join(parts)
print(full_description)  # "Japanese Ornamental Koi Fish"
```

### String Multiplication
```python
# Repeat a string
pattern = "Fish " * 3
print(pattern)  # "Fish Fish Fish "
```
