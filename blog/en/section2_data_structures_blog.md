# Python Data Structures: Building Your Programming Toolkit

*A conversation between Kurumi and Jarvis*

![Kurumi and Jarvis](../../assets/images/kurumi_jarvis_placeholder.jpg)

## Introduction to Data Structures

**Kurumi**: Jarvis, I've been practicing with variables and loops, but I'm still confused about how to organize larger amounts of data. Like, what if I want to keep track of all the fish in my pond?

**Jarvis**: That's a great question, Kurumi! This is where Python's data structures come in. Think of data structures as specialized containers that help you organize and manage collections of data efficiently.

**Kurumi**: Like different types of aquariums for different fish?

**Jarvis**: That's a perfect analogy! Just as different fish have different habitat needs, different types of data have different storage and access requirements. Python gives us four main built-in data structures: lists, tuples, sets, and dictionaries.

**Kurumi**: And I'm guessing each one has its own special purpose?

**Jarvis**: Exactly! Let's explore each one using our Japanese fish theme.

## Lists: Flexible Ordered Collections

**Kurumi**: So what's a list in Python?

**Jarvis**: A list is an ordered collection of items that can be modified. It's like a numbered fish tank where you can add, remove, or replace fish, and each fish has a specific position.

**Kurumi**: How do I create a list?

**Jarvis**: You use square brackets `[]` with items separated by commas. Let me show you:

```python
# Creating a list of Japanese fish
japanese_fish = ["Koi", "Fugu", "Tai", "Maguro", "Unagi"]
print(japanese_fish)
```

**Kurumi**: That's simple! How do I access specific fish in the list?

**Jarvis**: You use the index, which is the position number. Remember that Python starts counting from 0, not 1:

```python
first_fish = japanese_fish[0]  # "Koi"
third_fish = japanese_fish[2]  # "Tai"
last_fish = japanese_fish[-1]  # "Unagi" (negative indices count from the end)

print(f"First fish: {first_fish}")
print(f"Third fish: {third_fish}")
print(f"Last fish: {last_fish}")
```

**Kurumi**: What if I want to get several fish at once?

**Jarvis**: That's called slicing. You specify a range of indices:

```python
first_three = japanese_fish[0:3]  # ["Koi", "Fugu", "Tai"]
print(f"First three fish: {first_three}")
```

**Kurumi**: And how do I modify a list?

**Jarvis**: Lists are mutable, which means you can change them after creation. Here are some common operations:

```python
# Add a fish to the end
japanese_fish.append("Saba")  # Add mackerel
print(f"After append: {japanese_fish}")

# Insert a fish at a specific position
japanese_fish.insert(2, "Aji")  # Insert horse mackerel at index 2
print(f"After insert: {japanese_fish}")

# Replace a fish
japanese_fish[1] = "Hirame"  # Replace "Fugu" with "Hirame" (flounder)
print(f"After replacement: {japanese_fish}")

# Remove a fish
japanese_fish.remove("Tai")  # Remove sea bream
print(f"After remove: {japanese_fish}")

# Remove and return a fish at a specific position
removed_fish = japanese_fish.pop(3)  # Remove and return the fish at index 3
print(f"Removed fish: {removed_fish}")
print(f"After pop: {japanese_fish}")
```

**Kurumi**: That's a lot of operations! Are there other useful things I can do with lists?

**Jarvis**: Absolutely! You can sort them, count items, find positions, and more:

```python
fish_types = ["Tai", "Koi", "Fugu", "Koi", "Maguro"]

# Length of a list
print(f"Number of fish: {len(fish_types)}")

# Count occurrences
koi_count = fish_types.count("Koi")
print(f"Number of Koi: {koi_count}")

# Find index of an element
fugu_index = fish_types.index("Fugu")
print(f"Fugu is at index: {fugu_index}")

# Sorting
sorted_fish = sorted(fish_types)  # Creates a new sorted list
print(f"Sorted fish: {sorted_fish}")

fish_types.sort()  # Sorts the original list in-place
print(f"Original list sorted: {fish_types}")

# Checking if an element is in the list
has_koi = "Koi" in fish_types
print(f"Does the list contain Koi? {has_koi}")
```

**Kurumi**: I see! Lists seem really versatile. Is there a shortcut for creating lists with patterns?

**Jarvis**: Yes, Python has a powerful feature called list comprehensions that lets you create lists in a single line:

```python
# Traditional way
fish_lengths = []
for fish in ["Koi", "Fugu", "Tai", "Maguro", "Unagi"]:
    fish_lengths.append(len(fish))
print(f"Fish name lengths (traditional): {fish_lengths}")

# Using list comprehension
fish_lengths = [len(fish) for fish in ["Koi", "Fugu", "Tai", "Maguro", "Unagi"]]
print(f"Fish name lengths (comprehension): {fish_lengths}")

# List comprehension with condition
long_fish_names = [fish for fish in ["Koi", "Fugu", "Tai", "Maguro", "Unagi"] if len(fish) > 3]
print(f"Fish with names longer than 3 characters: {long_fish_names}")
```

**Kurumi**: That's so elegant! I love how compact it is.

## Tuples: Immutable Ordered Collections

**Jarvis**: Now let's talk about tuples. They're similar to lists but with one key difference: they're immutable, meaning once created, they cannot be changed.

**Kurumi**: Why would I want a container I can't modify?

**Jarvis**: Great question! Tuples are perfect for data that shouldn't change, like coordinates or database records. They're also slightly faster than lists and can be used as dictionary keys (which we'll cover later). You create them with parentheses `()`:

```python
# Creating a tuple
fish_info = ("Koi", 3, 2.5, "Freshwater")
print(fish_info)

# Accessing elements (similar to lists)
fish_name = fish_info[0]  # "Koi"
fish_age = fish_info[1]  # 3
print(f"Fish name: {fish_name}, Age: {fish_age}")
```

**Kurumi**: Can I unpack a tuple into separate variables?

**Jarvis**: Yes, that's a common and elegant way to use tuples:

```python
# Tuple unpacking
name, age, weight, habitat = fish_info
print(f"Name: {name}, Age: {age}, Weight: {weight}, Habitat: {habitat}")
```

**Kurumi**: What happens if I try to modify a tuple?

**Jarvis**: You'll get an error. Let's see:

```python
try:
    fish_info[0] = "Goldfish"  # This will raise an error
except TypeError as e:
    print(f"Error: {e}")
```

**Kurumi**: I see! So tuples are like sealed aquariums where the fish are fixed in place.

**Jarvis**: That's a perfect way to think about it!

## Sets: Unordered Collections of Unique Items

**Jarvis**: Next, let's explore sets. A set is an unordered collection of unique items. It's like a special tank that automatically removes duplicate fish and doesn't care about their order.

**Kurumi**: When would I use a set?

**Jarvis**: Sets are perfect when you need to ensure uniqueness or perform mathematical set operations like unions and intersections. They're created with curly braces `{}` or the `set()` constructor:

```python
# Creating a set
freshwater_fish = {"Koi", "Goldfish", "Unagi", "Koi"}  # Note: duplicates are removed
print(f"Freshwater fish set: {freshwater_fish}")  # Order is not guaranteed

# Creating a set from a list
saltwater_fish = set(["Tai", "Maguro", "Hirame", "Tai"])
print(f"Saltwater fish set: {saltwater_fish}")
```

**Kurumi**: How do I add or remove items from a set?

**Jarvis**: Like this:

```python
# Adding elements
freshwater_fish.add("Carp")
print(f"After adding Carp: {freshwater_fish}")

# Removing elements
freshwater_fish.remove("Unagi")  # Raises an error if the element is not present
print(f"After removing Unagi: {freshwater_fish}")

freshwater_fish.discard("Salmon")  # No error if the element is not present
print(f"After discarding Salmon (which wasn't in the set): {freshwater_fish}")
```

**Kurumi**: You mentioned set operations like in mathematics. Can you show me those?

**Jarvis**: Of course! These are very powerful features of sets:

```python
# Define two sets
freshwater_fish = {"Koi", "Goldfish", "Unagi", "Carp"}
aquarium_fish = {"Koi", "Goldfish", "Guppy", "Tetra"}

# Union: all elements from both sets
all_fish = freshwater_fish.union(aquarium_fish)
print(f"Union: {all_fish}")
# Alternative syntax: freshwater_fish | aquarium_fish

# Intersection: elements common to both sets
common_fish = freshwater_fish.intersection(aquarium_fish)
print(f"Intersection: {common_fish}")
# Alternative syntax: freshwater_fish & aquarium_fish

# Difference: elements in the first set but not in the second
only_freshwater = freshwater_fish.difference(aquarium_fish)
print(f"Difference (freshwater - aquarium): {only_freshwater}")
# Alternative syntax: freshwater_fish - aquarium_fish

# Symmetric difference: elements in either set, but not in both
unique_to_either = freshwater_fish.symmetric_difference(aquarium_fish)
print(f"Symmetric difference: {unique_to_either}")
# Alternative syntax: freshwater_fish ^ aquarium_fish
```

**Kurumi**: That's really useful! I can see how sets would be perfect for comparing different groups of fish.

## Dictionaries: Key-Value Pairs

**Jarvis**: The last major data structure is the dictionary. Dictionaries store key-value pairs, like a fish encyclopedia where each fish name (the key) is associated with information about that fish (the value).

**Kurumi**: How do I create a dictionary?

**Jarvis**: You use curly braces `{}` with colons `:` separating keys and values:

```python
# Creating a dictionary
fish_details = {
    "name": "Koi",
    "age": 3,
    "weight": 2.5,
    "colors": ["red", "white", "black"],
    "is_freshwater": True
}

print(fish_details)
```

**Kurumi**: How do I access values in a dictionary?

**Jarvis**: You use the key instead of an index:

```python
# Accessing by key
name = fish_details["name"]
print(f"Fish name: {name}")

# Using get() method (safer, provides a default if key doesn't exist)
age = fish_details.get("age")  # Returns None if key doesn't exist
print(f"Fish age: {age}")

price = fish_details.get("price", "Not for sale")  # Custom default value
print(f"Fish price: {price}")
```

**Kurumi**: What if I try to access a key that doesn't exist?

**Jarvis**: If you use square brackets and the key doesn't exist, you'll get a KeyError. That's why the `get()` method is often safer:

```python
try:
    price = fish_details["price"]  # This will raise a KeyError
except KeyError as e:
    print(f"Error: {e}")
```

**Kurumi**: How do I modify a dictionary?

**Jarvis**: You can add, update, or remove key-value pairs:

```python
# Adding a new key-value pair
fish_details["price"] = 5000  # yen
print(f"After adding price: {fish_details}")

# Updating an existing value
fish_details["weight"] = 2.7
print(f"After updating weight: {fish_details}")

# Removing a key-value pair
del fish_details["age"]
print(f"After deleting age: {fish_details}")

# Pop: remove and return a value
price = fish_details.pop("price")
print(f"Popped price: {price}")
print(f"After pop: {fish_details}")
```

**Kurumi**: Can I see all the keys or values in a dictionary?

**Jarvis**: Yes, dictionaries have methods for that:

```python
# Getting all keys
all_keys = fish_details.keys()
print(f"All keys: {all_keys}")

# Getting all values
all_values = fish_details.values()
print(f"All values: {all_values}")

# Getting all key-value pairs as tuples
all_items = fish_details.items()
print(f"All items: {all_items}")
```

**Kurumi**: How do I iterate through a dictionary?

**Jarvis**: There are several ways:

```python
fish_market = {
    "Maguro": 3000,  # yen per 100g
    "Tai": 2500,
    "Fugu": 5000,
    "Unagi": 4000
}

# Iterating through keys (default)
print("Available fish:")
for fish in fish_market:
    print(f"- {fish}")

# Iterating through values
print("\nPrices (yen per 100g):")
for price in fish_market.values():
    print(f"- {price}")

# Iterating through key-value pairs
print("\nFish market prices:")
for fish, price in fish_market.items():
    print(f"- {fish}: {price} yen per 100g")
```

**Kurumi**: Can dictionaries contain more complex data?

**Jarvis**: Absolutely! You can nest dictionaries within dictionaries, creating complex data structures:

```python
# Dictionary with nested dictionaries
fish_database = {
    "Koi": {
        "scientific_name": "Cyprinus rubrofuscus",
        "habitat": "Freshwater",
        "average_size": 60,  # cm
        "lifespan": 40,  # years
        "colors": ["red", "white", "black", "yellow", "blue"]
    },
    "Fugu": {
        "scientific_name": "Takifugu rubripes",
        "habitat": "Saltwater",
        "average_size": 40,  # cm
        "lifespan": 10,  # years
        "is_poisonous": True
    }
}

# Accessing nested dictionary values
koi_lifespan = fish_database["Koi"]["lifespan"]
print(f"Koi can live up to {koi_lifespan} years")

fugu_info = fish_database["Fugu"]
print(f"Fugu (scientific name: {fugu_info['scientific_name']}) is {'poisonous' if fugu_info['is_poisonous'] else 'not poisonous'}")
```

**Kurumi**: Is there something like list comprehensions for dictionaries?

**Jarvis**: Yes, dictionary comprehensions! They work similarly:

```python
# Creating a dictionary with comprehension
fish_lengths = {fish: len(fish) for fish in ["Koi", "Fugu", "Tai", "Maguro", "Unagi"]}
print(f"Fish name lengths: {fish_lengths}")

# Dictionary comprehension with condition
long_fish_lengths = {fish: len(fish) for fish in ["Koi", "Fugu", "Tai", "Maguro", "Unagi"] if len(fish) > 3}
print(f"Lengths of fish names longer than 3 characters: {long_fish_lengths}")
```

## String Operations and Formatting

**Kurumi**: We've talked about collections of data, but what about working with text? I know strings are important in Python.

**Jarvis**: Great point! Strings in Python are sequences of characters, and they have many powerful operations and methods.

**Kurumi**: What are some common string operations?

**Jarvis**: Let's go through the most useful ones:

```python
fish = "Maguro"  # Tuna in Japanese

# Length
print(f"Length of 'Maguro': {len(fish)}")

# Indexing and slicing (similar to lists)
first_char = fish[0]  # 'M'
last_char = fish[-1]  # 'o'
first_three = fish[0:3]  # 'Mag'

print(f"First character: {first_char}")
print(f"Last character: {last_char}")
print(f"First three characters: {first_three}")
```

**Kurumi**: What about changing the case or finding substrings?

**Jarvis**: Strings have many built-in methods for these operations:

```python
fish = "  Maguro Tuna  "

# Case methods
print(f"Original: '{fish}'")
print(f"Upper: '{fish.upper()}'")
print(f"Lower: '{fish.lower()}'")
print(f"Title: '{fish.title()}'")

# Whitespace removal
print(f"Strip: '{fish.strip()}'")
print(f"Left strip: '{fish.lstrip()}'")
print(f"Right strip: '{fish.rstrip()}'")

# Replacement
print(f"Replace 'Tuna' with 'Sashimi': '{fish.replace('Tuna', 'Sashimi')}'")

# Splitting
words = fish.strip().split()
print(f"Split into words: {words}")

# Joining
fish_list = ["Koi", "Fugu", "Tai", "Maguro"]
joined = ", ".join(fish_list)
print(f"Joined with commas: '{joined}'")

# Finding
text = "Japanese Koi Fish are popular in garden ponds"
position = text.find("Koi")
print(f"'Koi' found at position: {position}")

# Checking
print(f"Is 'Koi' alphabetic? {'Koi'.isalpha()}")
print(f"Is '123' numeric? {'123'.isdigit()}")
print(f"Is 'Koi123' alphanumeric? {'Koi123'.isalnum()}")
```

**Kurumi**: What about formatting strings with variables? I've seen you use f-strings, but are there other ways?

**Jarvis**: Yes, Python has several string formatting methods:

```python
name = "Koi"
age = 3
weight = 2.5

# %-formatting (older style)
old_style = "Fish: %s, Age: %d, Weight: %.1f kg" % (name, age, weight)
print(f"%-formatting: {old_style}")

# str.format() method
format_method = "Fish: {}, Age: {}, Weight: {:.1f} kg".format(name, age, weight)
print(f"str.format(): {format_method}")

# f-strings (Python 3.6+, recommended)
f_string = f"Fish: {name}, Age: {age}, Weight: {weight:.1f} kg"
print(f"f-string: {f_string}")
```

**Kurumi**: Which one should I use?

**Jarvis**: f-strings are the most modern, readable, and efficient method, so I recommend using them whenever possible. They were introduced in Python 3.6 and have become the standard way to format st<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>