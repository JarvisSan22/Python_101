# Section 3: Functions and Modularity

## Functions and Modules

### Introduction to Functions
- Reusable blocks of code that perform specific tasks
- Help organize code and avoid repetition
- Make code more readable and maintainable

### Defining Functions
```python
# Basic function definition
def greet_fish():
    print("Hello, fish world!")

# Function with parameters
def describe_fish(name, weight):
    print(f"This {name} weighs {weight} kg.")

# Function with default parameter values
def fish_status(name, is_freshwater=True):
    habitat = "freshwater" if is_freshwater else "saltwater"
    print(f"The {name} is a {habitat} fish.")
```

### Calling Functions
```python
# Calling a basic function
greet_fish()  # Output: Hello, fish world!

# Calling a function with arguments
describe_fish("Koi", 2.5)  # Output: This Koi weighs 2.5 kg.

# Using default parameter values
fish_status("Koi")  # Output: The Koi is a freshwater fish.
fish_status("Maguro", False)  # Output: The Maguro is a saltwater fish.

# Keyword arguments (order doesn't matter)
describe_fish(weight=3.2, name="Tai")  # Output: This Tai weighs 3.2 kg.
```

### Return Values
```python
# Function that returns a value
def calculate_fish_tank_volume(length, width, height):
    volume = length * width * height
    return volume

# Function that returns multiple values
def fish_stats(fish_list):
    count = len(fish_list)
    heaviest = max(fish_list, key=lambda x: x[1])
    return count, heaviest

# Using returned values
tank_volume = calculate_fish_tank_volume(100, 40, 30)  # in cm³
print(f"Tank volume: {tank_volume/1000} liters")

fish_data = [("Koi", 2.5), ("Tai", 1.8), ("Fugu", 3.2)]
count, (heaviest_name, heaviest_weight) = fish_stats(fish_data)
print(f"Total fish: {count}")
print(f"Heaviest fish: {heaviest_name}, {heaviest_weight} kg")
```

### Variable Scope
- Local variables: Defined inside a function, only accessible within that function
- Global variables: Defined outside functions, accessible throughout the file
- The `global` keyword allows modifying global variables from within functions

```python
# Global variable
total_fish = 0

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

### Lambda Functions
- Small anonymous functions defined with the `lambda` keyword
- Can take any number of arguments but have only one expression
- Useful for short, simple functions, especially as arguments to other functions

```python
# Regular function
def double(x):
    return x * 2

# Equivalent lambda function
double_lambda = lambda x: x * 2

print(double(5))        # 10
print(double_lambda(5)) # 10

# Lambda in sorting
fish_data = [("Koi", 2.5), ("Tai", 1.8), ("Fugu", 3.2)]
sorted_by_weight = sorted(fish_data, key=lambda fish: fish[1])
print(sorted_by_weight)  # [('Tai', 1.8), ('Koi', 2.5), ('Fugu', 3.2)]

# Lambda with filter
weights = [0.5, 1.2, 2.5, 3.0, 4.2]
large_fish = list(filter(lambda w: w > 2.0, weights))
print(large_fish)  # [2.5, 3.0, 4.2]
```

### Docstrings
- Documentation strings that describe what a function does
- Accessible via the `__doc__` attribute or the `help()` function
- Best practice for making code self-documenting

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

# Accessing the docstring
print(calculate_fish_tank_volume.__doc__)

# Or using help
help(calculate_fish_tank_volume)
```

---

### Introduction to Modules
- Modules are Python files containing code (functions, variables, classes)
- Allow organizing code into logical units
- Enable code reuse across different programs

### Importing Modules
```python
# Import the entire module
import math
radius = 5
area = math.pi * radius ** 2
print(f"Area of circle: {area}")

# Import specific items from a module
from math import pi, sqrt
area = pi * radius ** 2
diagonal = sqrt(10)
print(f"Area: {area}, Diagonal: {diagonal}")

# Import with an alias
import math as m
area = m.pi * radius ** 2
print(f"Area: {area}")

# Import all items from a module (not recommended in production code)
from math import *
area = pi * radius ** 2
print(f"Area: {area}")
```

### Creating Your Own Modules
- Any Python file can be a module
- Save functions, classes, and variables in a .py file
- Import them into other Python files

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

# In another file
import fish_utils

tank_vol = fish_utils.calculate_fish_tank_volume(100, 40, 30)
is_crowded = fish_utils.is_tank_overcrowded(tank_vol, 15)
print(f"Tank volume: {tank_vol} liters")
print(f"Is the tank overcrowded? {is_crowded}")
```

### The Standard Library
- Python comes with a rich standard library
- Provides modules for common tasks without additional installation
- Examples: math, random, datetime, os, sys, json, csv, etc.

```python
# Using the random module
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

# Using the datetime module
import datetime

now = datetime.datetime.now()
print(f"Current date and time: {now}")
print(f"Current year: {now.year}")
print(f"Current month: {now.month}")

# Date arithmetic
feeding_day = now + datetime.timedelta(days=3)
print(f"Next feeding day: {feeding_day}")
```

### Third-Party Modules
- Thousands of additional modules available via pip (Python's package manager)
- Extend Python's functionality for specific domains
- Examples: NumPy, Pandas, Matplotlib, Requests, etc.

```python
# Installing a third-party module
# pip install requests

# Using the requests module to fetch data from the web
import requests

response = requests.get("https://api.example.com/fish")
if response.status_code == 200:
    data = response.json()
    print(f"Received data: {data}")
else:
    print(f"Error: {response.status_code}")
```

### Module Search Path
- Python looks for modules in directories listed in `sys.path`
- Includes the current directory, standard library directories, and site-packages
- Can be modified to include custom directories

```python
import sys

# Print the module search path
for path in sys.path:
    print(path)

# Add a directory to the search path
sys.path.append("/path/to/custom/modules")
```

### Package Structure
- Packages are directories containing multiple module files
- Must include an `__init__.py` file (can be empty)
- Allow hierarchical organization of modules

```
fish_package/
    __init__.py
    freshwater.py
    saltwater.py
    utils.py
```

```python
# Importing from packages
from fish_package import freshwater
from fish_package.saltwater import tuna
import fish_package.utils as utils
```

## File Input/Output Operations

### Opening and Closing Files
```python
# Basic file opening and closing
file = open("fish_data.txt", "r")  # Open for reading
content = file.read()
file.close()  # Always close files when done

# Better approach using 'with' statement (automatically closes the file)
with open("fish_data.txt", "r") as file:
    content = file.read()
    # File is automatically closed when the block ends
```

### File Modes
- `"r"`: Read (default)
- `"w"`: Write (creates new file or truncates existing file)
- `"a"`: Append (adds to end of file)
- `"r+"`: Read and write
- `"b"`: Binary mode (add to other modes, e.g., `"rb"`, `"wb"`)

```python
# Writing to a file
with open("fish_list.txt", "w") as file:
    file.write("Koi\n")
    file.write("Fugu\n")
    file.write("Tai\n")

# Appending to a file
with open("fish_list.txt", "a") as file:
    file.write("Maguro\n")
    file.write("Unagi\n")

# Reading from a file
with open("fish_list.txt", "r") as file:
    content = file.read()
    print(content)
```

### Reading Files
```python
# Reading the entire file at once
with open("fish_data.txt", "r") as file:
    content = file.read()
    print(content)

# Reading line by line
with open("fish_data.txt", "r") as file:
    for line in file:
        print(line.strip())  # strip() removes trailing newline

# Reading all lines into a list
with open("fish_data.txt", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())

# Reading a specific number of characters
with open("fish_data.txt", "r") as file:
    chunk = file.read(10)  # Read first 10 characters
    print(chunk)
```

### Writing Files
```python
# Writing strings
with open("fish_report.txt", "w") as file:
    file.write("Fish Report\n")
    file.write("===========\n")
    file.write("Koi: 5\n")
    file.write("Fugu: 2\n")

# Writing multiple lines at once
lines = ["Tai: 3\n", "Maguro: 1\n", "Unagi: 4\n"]
with open("fish_report.txt", "a") as file:
    file.writelines(lines)
```

### Working with CSV Files
- CSV (Comma-Separated Values) is a common format for tabular data
- Python's `csv` module provides tools for reading and writing CSV files

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

# Using DictReader and DictWriter
fish_dict_data = [
    {"Name": "Koi", "Type": "Freshwater", "Weight (kg)": 2.5, "Price (yen)": 15000},
    {"Name": "Fugu", "Type": "Saltwater", "Weight (kg)": 3.2, "Price (yen)": 8000},
    {"Name": "Tai", "Type": "Saltwater", "Weight (kg)": 1.8, "Price (yen)": 5000}
]

with open("fish_dict.csv", "w", newline="") as file:
    fieldnames = ["Name", "Type", "Weight (kg)", "Price (yen)"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(fish_dict_data)

with open("fish_dict.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(f"{row['Name']}: {row['Weight (kg)']} kg, {row['Price (yen)']} yen")
```

### Working with JSON Files
- JSON (JavaScript Object Notation) is a popular data interchange format
- Python's `json` module provides tools for reading and writing JSON files

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
        "is_poisonous": True
    },
    "Tai": {
        "type": "Saltwater",
        "weight": 1.8,
        "price": 5000,
        "season": "Spring"
    }
}

# Writing JSON to a file
with open("fish_data.json", "w") as file:
    json.dump(fish_data, file, indent=4)  # indent for pretty-printing

# Reading JSON from a file
with open("fish_data.json", "r") as file:
    loaded_data = json.load(file)
    print(loaded_data["Koi"]["colors"])
    print(loaded_data["Fugu"]["is_poisonous"])

# Converting between JSON strings and Python objects
json_string = json.dumps(fish_data, indent=4)
print(json_string)

parsed_data = json.loads(json_string)
print(parsed_data["Tai"]["season"])
```

### File and Directory Operations
- The `os` module provides functions for interacting with the operating system
- Useful for file and directory operations

```python
import os

# Current working directory
cwd = os.getcwd()
print(f"Current directory: {cwd}")

# List files and directories
contents = os.listdir(cwd)
print(f"Directory contents: {contents}")

# Create a directory
os.mkdir("fish_data")
print("Created directory: fish_data")

# Check if a file exists
if os.path.exists("fish_list.txt"):
    print("fish_list.txt exists")

# File information
if os.path.isfile("fish_list.txt"):
    size = os.path.getsize("fish_list.txt")
    print(f"File size: {size} bytes")
    
    mod_time = os.path.getmtime("fish_list.txt")
    import time
    print(f"Last modified: {time.ctime(mod_time)}")

# Rename a file
os.rename("fish_list.txt", "japanese_fish.txt")
print("Renamed file to japanese_fish.txt")

# Remove a file
os.remove("japanese_fish.txt")
print("Removed japanese_fish.txt")

# Remove a directory
os.rmdir("fish_data")
print("Removed directory: fish_data")
```

### Working with Paths
- The `os.path` module provides functions for manipulating file paths
- The `pathlib` module (Python 3.4+) offers an object-oriented approach to paths

```python
import os.path

# Join path components
data_dir = "fish_data"
file_name = "koi.txt"
full_path = os.path.join(data_dir, file_name)
print(f"Full path: {full_path}")

# Split a path into directory and file
directory, file = os.path.split(full_path)
print(f"Directory: {directory}, File: {file}")

# Get file extension
name, ext = os.path.splitext(file_name)
print(f"Name: {name}, Extension: {ext}")

# Using pathlib (more modern approach)
from pathlib import Path

data_path = Path("fish_data")
file_path = data_path / "koi.txt"  # Path joining with / operator
print(f"File path: {file_path}")

# Creating directories
data_path.mkdir(exist_ok=True)  # Won't error if directory exists

# Checking if a file exists
if file_path.exists():
    print(f"{file_path} exists")
else:
    print(f"{file_path} does not exist")

# Iterating over files in a directory
for file in data_path.glob("*.txt"):  # All .txt files
    print(file)
```

## Understanding main() and \_\_name\_\_

### The \_\_name\_\_ Variable
- Special variable set by Python interpreter
- Equals `"__main__"` when the file is run directly
- Equals the module name when the file is imported

```python
# fish_module.py
print(f"The value of __name__ is: {__name__}")

def main():
    print("Running the main function in fish_module.py")

if __name__ == "__main__":
    print("This file is being run directly")
    main()
else:
    print("This file is being imported as a module")
```

### Using if \_\_name\_\_ == "\_\_main\_\_":
- Common pattern to make a file both importable and executable
- Code inside this block only runs when the file is executed directly
- Allows for testing code within modules

```python
# fish_calculator.py
def calculate_fish_tank_volume(length, width, height):
    """Calculate the volume of a rectangular fish tank in liters."""
    volume_cm3 = length * width * height
    volume_liters = volume_cm3 / 1000
    return volume_liters

def is_tank_overcrowded(tank_volume, fish_count, liters_per_fish=10):
    """Check if a tank is overcrowded based on the recommende<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>