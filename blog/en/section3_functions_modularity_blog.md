# Python Functions and Modularity: Building Reusable Code

*A conversation between Kurumi and Jarvis*

![Kurumi and Jarvis](../../assets/images/kurumi_jarvis_placeholder.jpg)

## Introduction to Functions

**Kurumi**: Jarvis, I've been writing Python code following our previous lessons, but I'm noticing that I keep writing the same code over and over again. Is there a better way to organize my code?

**Jarvis**: That's a great observation, Kurumi! You've just identified one of the fundamental principles of good programming: Don't Repeat Yourself, or DRY for short. Python provides functions to help us avoid repetition and organize our code better.

**Kurumi**: Functions? Like mathematical functions?

**Jarvis**: Similar concept, but more powerful. A function in programming is a reusable block of code that performs a specific task. Think of it like a recipe for a specific dish that you can use whenever you need it.

**Kurumi**: That sounds useful! How do I create a function in Python?

**Jarvis**: You define a function using the `def` keyword, followed by the function name, parentheses, and a colon. The function body is indented. Let me show you a simple example:

```python
def greet_fish():
    print("Hello, fish world!")

# Now we can call this function whenever we need it
greet_fish()  # Output: Hello, fish world!
greet_fish()  # Output: Hello, fish world!
```

**Kurumi**: I see! So instead of writing the print statement multiple times, I can just call the function. But what if I want to greet different fish?

## Functions with Parameters

**Jarvis**: Great question! Functions become even more powerful when they can accept inputs, which we call parameters or arguments. Let's modify our function:

```python
def greet_fish(fish_name):
    print(f"Hello, {fish_name}!")

# Now we can greet different fish
greet_fish("Koi")      # Output: Hello, Koi!
greet_fish("Fugu")     # Output: Hello, Fugu!
greet_fish("Maguro")   # Output: Hello, Maguro!
```

**Kurumi**: That's much more flexible! Can a function have multiple parameters?

**Jarvis**: Absolutely! You can add as many parameters as you need, separated by commas:

```python
def describe_fish(name, weight, habitat):
    print(f"The {name} weighs {weight} kg and lives in {habitat} water.")

# Using the function with multiple arguments
describe_fish("Koi", 2.5, "fresh")
# Output: The Koi weighs 2.5 kg and lives in fresh water.

describe_fish("Maguro", 80, "salt")
# Output: The Maguro weighs 80 kg and lives in salt water.
```

**Kurumi**: What if I don't always have all that information? Do I always need to provide all the parameters?

**Jarvis**: You can make parameters optional by providing default values:

```python
def fish_status(name, is_freshwater=True):
    habitat = "freshwater" if is_freshwater else "saltwater"
    print(f"The {name} is a {habitat} fish.")

# Using default parameter
fish_status("Koi")  # Output: The Koi is a freshwater fish.

# Overriding default parameter
fish_status("Maguro", False)  # Output: The Maguro is a saltwater fish.
```

**Kurumi**: That's convenient! Are there other ways to make function calls more readable?

**Jarvis**: Yes, you can use keyword arguments, where you explicitly specify which parameter each value is for:

```python
describe_fish(name="Tai", weight=1.8, habitat="salt")
# Output: The Tai weighs 1.8 kg and lives in salt water.

# The order doesn't matter with keyword arguments
describe_fish(habitat="salt", name="Fugu", weight=3.2)
# Output: The Fugu weighs 3.2 kg and lives in salt water.
```

**Kurumi**: That makes the code much clearer, especially when there are many parameters!

## Return Values

**Kurumi**: So far, our functions just print things. Can functions give back results that I can use in other calculations?

**Jarvis**: Absolutely! Functions can return values using the `return` statement. This is one of the most powerful aspects of functions:

```python
def calculate_fish_tank_volume(length, width, height):
    volume = length * width * height
    return volume

# Using the returned value
tank_volume = calculate_fish_tank_volume(100, 40, 30)  # in cm³
print(f"Tank volume: {tank_volume} cm³")
print(f"Tank volume: {tank_volume/1000} liters")
```

**Kurumi**: So the function calculates the volume and gives it back to us, and then we can use that value however we want?

**Jarvis**: Exactly! The function does its specific job and returns the result, which you can then use in other parts of your program. Functions can even return multiple values:

```python
def fish_stats(fish_list):
    count = len(fish_list)
    heaviest = max(fish_list, key=lambda x: x[1])
    return count, heaviest

# Using returned values
fish_data = [("Koi", 2.5), ("Tai", 1.8), ("Fugu", 3.2)]
count, (heaviest_name, heaviest_weight) = fish_stats(fish_data)
print(f"Total fish: {count}")
print(f"Heaviest fish: {heaviest_name}, {heaviest_weight} kg")
```

**Kurumi**: Wait, what's that `lambda` thing in there?

**Jarvis**: Good catch! That's a lambda function, which is a small anonymous function. We'll talk more about those later. For now, just know that it's telling the `max()` function to compare the fish based on their weights.

## Variable Scope

**Kurumi**: I've noticed something strange. Sometimes when I create a variable inside a function, I can't access it outside. Why is that?

**Jarvis**: That's because of variable scope. Variables defined inside a function are local to that function and can't be accessed from outside. This is actually a good thing because it prevents functions from accidentally interfering with each other.

```python
def add_fish_to_tank():
    fish_name = "Koi"  # Local variable
    print(f"Added {fish_name} to tank")

add_fish_to_tank()
# This would cause an error because fish_name only exists inside the function
# print(fish_name)
```

**Kurumi**: What if I want a variable that can be accessed from anywhere?

**Jarvis**: That would be a global variable, which is defined outside any function. Functions can access global variables, but they need special permission to modify them:

```python
total_fish = 0  # Global variable

def add_fish(count):
    # This creates a local variable, not modifying the global one
    total_fish = count
    print(f"Local total_fish: {total_fish}")

def add_fish_global(count):
    # This modifies the global variable
    global total_fish
    total_fish += count
    print(f"Global total_fish: {total_fish}")

add_fish(5)
print(f"After add_fish: {total_fish}")  # Still 0

add_fish_global(5)
print(f"After add_fish_global: {total_fish}")  # Now 5
```

**Kurumi**: I see! So I need to use the `global` keyword if I want to modify a global variable from within a function.

**Jarvis**: Exactly. But as a best practice, try to limit your use of global variables. It's usually better to pass values as parameters and return results, as it makes your code more predictable and easier to test.

## Lambda Functions

**Kurumi**: You mentioned lambda functions earlier. What are they exactly?

**Jarvis**: Lambda functions are small, anonymous functions defined with the `lambda` keyword. They can take any number of arguments but can only have one expression. They're useful for short, simple functions, especially when you need to pass a function as an argument to another function.

```python
# Regular function
def double(x):
    return x * 2

# Equivalent lambda function
double_lambda = lambda x: x * 2

print(double(5))        # 10
print(double_lambda(5)) # 10
```

**Kurumi**: When would I use a lambda function instead of a regular function?

**Jarvis**: Lambda functions are particularly useful with functions like `sorted()`, `filter()`, and `map()`. For example:

```python
# Sorting a list of fish tuples by weight
fish_data = [("Koi", 2.5), ("Tai", 1.8), ("Fugu", 3.2)]
sorted_by_weight = sorted(fish_data, key=lambda fish: fish[1])
print(sorted_by_weight)  # [('Tai', 1.8), ('Koi', 2.5), ('Fugu', 3.2)]

# Filtering a list to keep only large fish
weights = [0.5, 1.2, 2.5, 3.0, 4.2]
large_fish = list(filter(lambda w: w > 2.0, weights))
print(large_fish)  # [2.5, 3.0, 4.2]

# Mapping a list of weights from kg to pounds
weights_in_pounds = list(map(lambda kg: kg * 2.20462, weights))
print(weights_in_pounds)  # [1.10231, 2.645544, 5.51155, 6.61386, 9.259404]
```

**Kurumi**: I see! Lambda functions are perfect for these short, one-time operations.

## Docstrings and Code Documentation

**Kurumi**: How do I document what my functions do, so I remember later or so others can understand my code?

**Jarvis**: Great question! Python has a convention called docstrings, which are strings that describe what a function does. They're placed right after the function definition, before the code:

```python
def calculate_fish_tank_volume(length, width, height):
    """
    Calculate the volume of a rectangular fish tank.
    
    Args:
        length (float): Length of the tank in centimeters
        width (float): Width of the tank in centimeters
        height (float): Height of the tank in centimeters
        
    Returns:
        float: Volume of the tank in cubic centimeters
    """
    volume = length * width * height
    return volume
```

**Kurumi**: That's really helpful! How do I access these docstrings?

**Jarvis**: You can access a function's docstring using the `__doc__` attribute or the `help()` function:

```python
print(calculate_fish_tank_volume.__doc__)
# or
help(calculate_fish_tank_volume)
```

**Kurumi**: I'll make sure to add docstrings to all my functions from now on!

## Introduction to Modules

**Kurumi**: My code is getting longer and more complex. Is there a way to organize it into separate files?

**Jarvis**: Absolutely! That's where modules come in. A module is simply a Python file containing code that can be imported and used in other Python files. This helps organize code into logical units and enables code reuse across different programs.

**Kurumi**: How do I create and use a module?

**Jarvis**: Let's say we create a file called `fish_utils.py` with some useful functions:

```python
# fish_utils.py
def calculate_fish_tank_volume(length, width, height):
    """Calculate the volume of a rectangular fish tank in liters."""
    volume_cm3 = length * width * height
    volume_liters = volume_cm3 / 1000
    return volume_liters

def is_tank_overcrowded(tank_volume, fish_count, liters_per_fish=10):
    """Check if a tank is overcrowded based on the recommended water volume per fish."""
    return tank_volume < fish_count * liters_per_fish

# Constants
FRESHWATER_FISH = ["Koi", "Goldfish", "Guppy"]
SALTWATER_FISH = ["Tai", "Maguro", "Fugu"]
```

Then in another file, we can import and use these functions:

```python
# main.py
import fish_utils

# Calculate tank volume
tank_vol = fish_utils.calculate_fish_tank_volume(100, 40, 30)
print(f"Tank volume: {tank_vol:.2f} liters")

# Check if tank is overcrowded
fish_count = 15
is_crowded = fish_utils.is_tank_overcrowded(tank_vol, fish_count)
print(f"Is the tank overcrowded with {fish_count} fish? {is_crowded}")

# Use the constants
print(f"Freshwater fish: {fish_utils.FRESHWATER_FISH}")
print(f"Saltwater fish: {fish_utils.SALTWATER_FISH}")
```

**Kurumi**: That's really neat! Are there different ways to import modules?

**Jarvis**: Yes, there are several import styles:

```python
# Import the entire module
import fish_utils

# Import specific items from a module
from fish_utils import calculate_fish_tank_volume, FRESHWATER_FISH

# Import with an alias
import fish_utils as fu

# Import all items from a module (not recommended in production code)
from fish_utils import *
```

**Kurumi**: Which style is best?

**Jarvis**: It depends on the situation, but generally:
- Use `import module` when you're using several things from the module
- Use `from module import item` when you're only using a few specific items
- Use `import module as alias` when the module name is long or conflicts with other names
- Avoid `from module import *` in production code as it can lead to naming conflicts and make it unclear where functions are coming from

## The Standard Library

**Kurumi**: Do I always have to create my own modules, or does Python come with some built-in ones?

**Jarvis**: Python comes with a rich standard library that provides modules for many common tasks. Let's look at a few examples:

### The `random` Module

```python
import random

# Random number between 0 and 1
print(random.random())

# Random integer in range
fish_count = random.randint(1, 10)
print(f"Random fish count: {fish_count}")

# Random choice from a sequence
fish_types = ["Koi", "Fugu", "Tai", "Maguro", "Unagi"]
selected_fish = random.choice(fish_types)
print(f"Randomly selected fish: {selected_fish}")

# Shuffle a list
random.shuffle(fish_types)
print(f"Shuffled fish list: {fish_types}")
```

### The `datetime` Module

```python
import datetime

now = datetime.datetime.now()
print(f"Current date and time: {now}")
print(f"Current year: {now.year}")
print(f"Current month: {now.month}")

# Date arithmetic
feeding_day = now + datetime.timedelta(days=3)
print(f"Next feeding day: {feeding_day}")
```

### The `math` Module

```python
import math

# Constants
print(f"Pi: {math.pi}")
print(f"Euler's number: {math.e}")

# Functions
print(f"Square root of 16: {math.sqrt(16)}")
print(f"Sine of 30 degrees: {math.sin(math.radians(30))}")
```

**Kurumi**: These are really useful! Are there modules for working with files too?

## File Input/Output Operations

**Jarvis**: Yes, Python has built-in functions for working with files. Let's start with the basics:

### Writing to Files

```python
# Writing to a file
with open("fish_list.txt", "w") as file:
    file.write("Koi\n")  # \n is a newline character
    file.write("Fugu\n")
    file.write("Tai\n")
    file.write("Maguro\n")
    file.write("Unagi\n")

print("File written successfully!")
```

### Reading from Files

```python
# Reading the entire file at once
with open("fish_list.txt", "r") as file:
    content = file.read()
    print("File content:")
    print(content)

# Reading line by line
with open("fish_list.txt", "r") as file:
    print("Reading line by line:")
    for line in file:
        print(f"- {line.strip()}")  # strip() removes trailing newline
```

**Kurumi**: What's that `with` statement you're using?

**Jarvis**: The `with` statement is a context manager that automatically takes care of closing the file when you're done with it. It's the recommended way to work with files in Python because it ensures proper resource management even if an error occurs.

**Kurumi**: What if I want to add more fish to my list without overwriting the existing ones?

**Jarvis**: You can open the file in append mode using the `"a"` flag:

```python
# Appending to a file
with open("fish_list.txt", "a") as file:
    file.write("Saba\n")  # Adding mackerel
    file.write("Hirame\n")  # Adding flounder

print("File updated!")
```

**Kurumi**: What about working with more structured data, like tables or JSON?

**Jarvis**: Python has modules for that too! Let's look at CSV and JSON:

### Working with CSV Files

```python
import csv

# Writing CSV data
fish_data = [
    ["Name", "Type", "Weight (kg)", "Price (yen)"],
    ["Koi", "Freshwater", 2.5, 15000],
    ["Fugu", "Saltwater", 3.2, 8000],
    ["Tai", "Saltwater", 1.8, 5000],
    ["Unagi", "Freshwater", 1.2, 4000]
]

with open("fish_inventory.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(fish_data)

# Reading CSV data
with open("fish_inventory.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(", ".join(row))
```

### Working with JSON Files

```python
import json

# Python dictionary
fish_data = {
    "Koi": {
        "type": "Freshwater",
        "weight": 2.5,
        "price": 15000,
        "colors": ["red", "white", "black"]
    },
    "Fugu": {
        "type": "Saltwater",
        "weight": 3.2,
        "price": 8000,
        "is<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>