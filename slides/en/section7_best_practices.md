# Section 7: Python Best Practices

## Introduction to Python's pep8 style guide

### What is PEP 8?
- PEP 8 is Python's official style guide
- Created to improve code readability and consistency
- Followed by most Python developers and projects
- Not enforced by the interpreter, but widely adopted by the community

### Why Follow a Style Guide?
- Improves code readability
- Makes collaboration easier
- Reduces cognitive load when reading code
- Helps maintain consistency across projects
- Makes code more professional and maintainable

### Code Layout

#### Indentation
```python
# Use 4 spaces per indentation level
def calculate_fish_weight(length, species):
    if species == "Koi":
        weight = length * 0.8
        return weight
    else:
        weight = length * 0.5
        return weight
```

#### Maximum Line Length
```python
# Limit lines to 79 characters for code
# Limit lines to 72 characters for docstrings and comments

# Bad - line too long
fish_species = ["Koi", "Fugu", "Tai", "Unagi", "Saba", "Maguro", "Hamachi", "Sake", "Hirame", "Ika", "Hotate", "Amaebi", "Ikura", "Uni", "Anago"]

# Good - line broken appropriately
fish_species = [
    "Koi", "Fugu", "Tai", "Unagi", "Saba",
    "Maguro", "Hamachi", "Sake", "Hirame", "Ika",
    "Hotate", "Amaebi", "Ikura", "Uni", "Anago"
]

# For long expressions
total_weight = (koi_weight + fugu_weight + tai_weight +
                unagi_weight + saba_weight)
```

#### Line Breaks and Binary Operators
```python
# Recommended style - break before operators
income = (gross_wages
          + taxable_interest
          + dividends)

# Alternative style - break after operators
income = gross_wages + \
         taxable_interest + \
         dividends
```

#### Blank Lines
```python
# Use blank lines to separate logical sections
def calculate_fish_weight(length, species):
    """Calculate fish weight based on length and species."""
    if species == "Koi":
        factor = 0.8
    else:
        factor = 0.5
    
    weight = length * factor
    return weight


def calculate_fish_price(weight, species):
    """Calculate fish price based on weight and species."""
    if species == "Fugu":
        price_per_kg = 5000
    else:
        price_per_kg = 2000
    
    price = weight * price_per_kg
    return price
```

#### Imports
```python
# Imports should be on separate lines
import os
import sys

# Not like this
import os, sys

# Imports should be grouped in the following order:
# 1. Standard library imports
# 2. Related third party imports
# 3. Local application/library specific imports

# Standard library imports
import os
import sys
import math

# Third party imports
import numpy as np
import pandas as pd

# Local application imports
import fish_calculator
from fish_database import FishDB
```

### String Quotes
```python
# Single quotes and double quotes are treated the same
# Be consistent within a project
fish_name = 'Koi'
fish_type = "Freshwater"

# Use the other quote style to avoid escaping
message = "Don't forget to feed the fish"
query = 'SELECT * FROM fish WHERE name = "Koi"'
```

### Whitespace

#### Whitespace in Expressions and Statements
```python
# Yes: Good use of whitespace
x = 1
y = 2
long_variable = 3

# No: Bad use of whitespace
x=1
y = 2
long_variable=3

# Yes: Good use of whitespace in expressions
i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)

# No: Bad use of whitespace in expressions
i=i+1
submitted +=1
x = x * 2-1
hypot2 = x * x+y * y
c = (a + b)*(a - b)
```

#### Whitespace in Function Calls
```python
# Yes: Good use of whitespace in function calls
function(arg1, arg2)
function(key=value)
function(key1=value1, key2=value2)

# No: Bad use of whitespace in function calls
function ( arg1, arg2 )
function(arg1,arg2)
function(key = value)
function(key1 = value1,key2 = value2)
```

#### Whitespace in Slices
```python
# Yes: Good use of whitespace in slices
fish_list[0]
fish_list[1:3]
fish_list[1:3:2]
fish_list[:3]
fish_list[3:]
fish_list[:]

# No: Bad use of whitespace in slices
fish_list[ 0 ]
fish_list[1 : 3]
fish_list[1 : 3 : 2]
```

### Comments

#### Block Comments
```python
# This is a block comment that describes
# a complex piece of code that follows.
# Each line starts with a # and a space.

complex_code_here()
```

#### Inline Comments
```python
x = x + 1  # Increment x by 1
```

#### Documentation Strings (Docstrings)
```python
def calculate_fish_weight(length, species):
    """
    Calculate the weight of a fish based on its length and species.
    
    Args:
        length (float): The length of the fish in centimeters.
        species (str): The species of the fish.
        
    Returns:
        float: The calculated weight in kilograms.
    """
    if species == "Koi":
        factor = 0.8
    else:
        factor = 0.5
    
    weight = length * factor
    return weight
```

### Naming Conventions

#### General Naming Guidelines
- Names should be descriptive and meaningful
- Avoid single-letter names except for counters or iterators
- Avoid names that could be confused with built-in functions or keywords

#### Naming Styles
```python
# Module names: short, lowercase, underscores if needed
import fish_database

# Package names: short, lowercase, no underscores
import fishdata

# Class names: CapWords (CamelCase)
class FishDatabase:
    pass

# Function and variable names: lowercase with underscores
def calculate_fish_weight():
    fish_length = 25
    
# Method names: lowercase with underscores
class Fish:
    def get_weight(self):
        pass
    
# Constants: ALL_UPPERCASE with underscores
MAX_FISH_LENGTH = 100
PI = 3.14159
```

#### Naming Conventions for Special Methods
```python
class Fish:
    def __init__(self, name, weight):
        self.name = name
        self.weight = weight
    
    def __str__(self):
        return f"{self.name}: {self.weight} kg"
    
    def __eq__(self, other):
        return self.weight == other.weight
```

### Programming Recommendations

#### Comparisons
```python
# Yes: Good comparisons
if x is None:
    # do something
    
if x is not None:
    # do something else

# No: Bad comparisons
if x == None:
    # don't do this
    
if x != None:
    # don't do this either
```

#### Boolean Checks
```python
# Yes: Good boolean checks
if fish_list:  # Checks if list is non-empty
    # do something
    
if not fish_list:  # Checks if list is empty
    # do something else

# No: Bad boolean checks
if len(fish_list) > 0:  # Unnecessarily verbose
    # avoid this
    
if len(fish_list) == 0:  # Unnecessarily verbose
    # avoid this too
```

#### Return Statements
```python
# Yes: Consistent return statements
def is_large_fish(weight):
    if weight > 5:
        return True
    return False

# Better: Simplified return
def is_large_fish(weight):
    return weight > 5

# No: Inconsistent return types
def get_fish_size(weight):
    if weight > 5:
        return "large"
    elif weight > 2:
        return "medium"
    else:
        return 0  # Inconsistent return type (string vs int)
```

#### String Formatting
```python
# Old style (not recommended for new code)
fish_info = "%s: %.1f kg" % (name, weight)

# str.format() method
fish_info = "{}: {:.1f} kg".format(name, weight)

# f-strings (Python 3.6+, recommended)
fish_info = f"{name}: {weight:.1f} kg"
```

#### Error Handling
```python
# Yes: Specific exception handling
try:
    with open("fish_data.txt") as f:
        data = f.read()
except FileNotFoundError:
    print("File not found")
except PermissionError:
    print("Permission denied")

# No: Bare except clause
try:
    with open("fish_data.txt") as f:
        data = f.read()
except:  # This will catch all exceptions, including KeyboardInterrupt
    print("An error occurred")
```

### Using Tools to Check PEP 8 Compliance

#### Linters and Formatters
- **pycodestyle** (formerly pep8): Checks code against PEP 8
- **pylint**: More comprehensive linter that includes PEP 8 checks
- **flake8**: Combines pycodestyle with other tools
- **black**: Automatic code formatter
- **autopep8**: Automatic code formatter focused on PEP 8

#### Example: Using pycodestyle
```bash
# Install pycodestyle
pip install pycodestyle

# Check a file
pycodestyle fish_calculator.py

# Check a directory
pycodestyle fish_project/
```

#### Example: Using black
```bash
# Install black
pip install black

# Format a file
black fish_calculator.py

# Format a directory
black fish_project/
```

## Working with .py Files

### Creating Python Modules

#### What is a Module?
- A module is a file containing Python definitions and statements
- Used to organize related code into a single file
- Allows code reuse across multiple scripts

#### Creating a Simple Module
```python
# fish_utils.py
"""Utility functions for working with fish data."""

def calculate_weight(length, species):
    """Calculate fish weight based on length and species."""
    if species == "Koi":
        factor = 0.8
    else:
        factor = 0.5
    
    return length * factor

def calculate_price(weight, species):
    """Calculate fish price based on weight and species."""
    if species == "Fugu":
        price_per_kg = 5000
    else:
        price_per_kg = 2000
    
    return weight * price_per_kg

# Constants
FRESHWATER_SPECIES = ["Koi", "Unagi"]
SALTWATER_SPECIES = ["Fugu", "Tai", "Saba"]
```

#### Importing Modules
```python
# Importing the entire module
import fish_utils

weight = fish_utils.calculate_weight(25, "Koi")
price = fish_utils.calculate_price(weight, "Koi")

# Importing specific functions
from fish_utils import calculate_weight, calculate_price

weight = calculate_weight(25, "Koi")
price = calculate_price(weight, "Koi")

# Importing with an alias
import fish_utils as fu

weight = fu.calculate_weight(25, "Koi")
price = fu.calculate_price(weight, "Koi")

# Importing all functions (not recommended)
from fish_utils import *

weight = calculate_weight(25, "Koi")
price = calculate_price(weight, "Koi")
```

### Creating Python Packages

#### What is a Package?
- A package is a directory containing Python modules
- Used to organize related modules into a directory hierarchy
- Must contain a special file called `__init__.py`

#### Basic Package Structure
```
fish_package/
├── __init__.py
├── fish_utils.py
├── fish_database.py
└── fish_analysis.py
```

#### The `__init__.py` File
```python
# fish_package/__init__.py
"""Fish package for fish-related utilities."""

# Import commonly used functions to make them available directly
from .fish_utils import calculate_weight, calculate_price
```

#### Importing from Packages
```python
# Importing the package
import fish_package

# Using functions imported in __init__.py
weight = fish_package.calculate_weight(25, "Koi")

# Importing a specific module from the package
from fish_package import fish_database

db = fish_database.FishDB()

# Importing specific functions from a module in the package
from fish_package.fish_analysis import analyze_weights, plot_distribution
```

### Running Python Scripts

#### Making Scripts Executable
```python
#!/usr/bin/env python3
"""
A script to analyze fish data.
"""

import sys
from fish_package import fish_utils

def main():
    """Main function to run the script."""
    if len(sys.argv) < 3:
        print("Usage: python analyze_fish.py <length> <species>")
        sys.exit(1)
    
    length = float(sys.argv[1])
    species = sys.argv[2]
    
    weight = fish_utils.calculate_weight(length, species)
    price = fish_utils.calculate_price(weight, species)
    
    print(f"Fish: {species}")
    print(f"Length: {length} cm")
    print(f"Weight: {weight:.2f} kg")
    print(f"Price: {price:.2f} yen")

if __name__ == "__main__":
    main()
```

#### Running Scripts from the Command Line
```bash
# Run a script
python analyze_fish.py 25 Koi

# Make a script executable (Unix/Linux/Mac)
chmod +x analyze_fish.py
./analyze_fish.py 25 Koi
```

## Understanding main() and __name__

### The `__name__` Variable
- `__name__` is a built-in variable in Python
- Set to `"__main__"` when the script is run directly
- Set to the module's name when the script is imported

### The `if __name__ == "__main__":` Pattern
```python
# fish_analyzer.py
"""Module for analyzing fish data."""

def analyze_fish(length, species):
    """Analyze fish data and return results."""
    # ... analysis code here ...
    return results

def main():
    """Run the main function when script is executed directly."""
    print("Running fish analyzer...")
    results = analyze_fish(25, "Koi")
    print(results)

if __name__ == "__main__":
    main()
```

### Why Use This Pattern?
- Allows a file to be both a module and a script
- Code in the `main()` function only runs when the file is executed directly
- When the file is imported as a module, only the functions and classes are defined
- Enables code reuse and testing

### Example: Module vs. Script
```python
# When run as a script:
# $ python fish_analyzer.py
# Output:
# Running fish analyzer...
# (analysis results)

# When imported as a module:
# >>> import fish_analyzer
# >>> fish_analyzer.analyze_fish(25, "Koi")
# (analysis results)
# Note: The main() function is not called automatically
```

## Command Line Arguments (sys.argv)

### Introduction to sys.argv
- `sys.argv` is a list containing command line arguments
- `sys.argv[0]` is the script name
- `sys.argv[1]` onwards are the arguments passed to the script

### Basic Usage
```python
import sys

print("Script name:", sys.argv[0])
print("Arguments:", sys.argv[1:])

# If run as: python script.py arg1 arg2 arg3
# Output:
# Script name: script.py
# Arguments: ['arg1', 'arg2', 'arg3']
```

### Parsing Command Line Arguments
```python
import sys

def main():
    if len(sys.argv) < 3:
        print("Usage: python fish_calculator.py <length> <species>")
        sys.exit(1)
    
    try:
        length = float(sys.argv[1])
        species = sys.argv[2]
        
        # Process the arguments
        print(f"Calculating for {species} with length {length} cm")
        
    except ValueError:
        print("Error: Length must be a number")
        sys.exit(1)

if __name__ == "__main__":
    main()
```

### Using argparse for Better Argument Handling
```python
import argparse

def main():
    parser = argparse.ArgumentParser(description="Calculate fish weight and price.")
    
    parser.add_argument("length", type=float, help="Fish length in centimeters")
    parser.add_argument("species", help="Fish species (e.g., Koi, Fugu)")
    parser.add_argument("--unit", choices=["cm", "inch"], default="cm",
                        help="Unit of length (default: cm)")
    parser.add_argument("--verbose", "-v", action="store_true",
                        help="Print detailed information")
    
    args = parser.parse_args()
    
    # Convert inches to cm if needed
    if args.unit == "inch":
        length_cm = args.length * 2.54
    else:
        length_cm = args.length
    
    # Process the arguments
    if args.verbose:
        print(f"Processing {args.species} with length {length_cm} cm")
    
    # Calculate weight and price
    # ...

if __name__ == "__main__":
    main()
```

### Running with Different Arguments
```bash
# Basic usage
python fish_calculator.py 25 Koi

# With optional arguments
python fish_calculator.py 10 Fugu --unit inch
python fish_calculator.py 25 Koi --verbose
```

## Project Structure and Organization in Python

### Basic Project Structure
```
my_project/
├── README.md
├── LICENSE
├── setup.py
├── requirements.txt
├── my_package/
│   ├── __init__.py
│   ├── module1.py
│   ├── module2.py
│   └── subpackage/
│       ├── __init__.py
│       └── module3.py
├── tests/
│   ├── __init__.py
│   ├── test_module1.py
│   └── test_module2.py
├── docs/
│   ├── conf.py
│   └── index.rst
└── examples/
    ├── example1.py
    └── example2.py
```

### Key Components

#### README.md
```markdown
# Fish Analysis Package

A Python package for analyzing fish data.

## Installation

```bash
pip instal<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>