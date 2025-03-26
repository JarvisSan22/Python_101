# Section 7: Python Best Practices - Homework Assignments

## PEP 8 Style Guide

### Exercise 1: Code Formatting
1. The following code violates several PEP 8 guidelines. Identify and fix all the style issues:

```python
class fish:
    def __init__(self,name,weight,species,habitat):
        self.name=name
        self.weight=weight
        self.species=species
        self.habitat=habitat
    def calculate_price(self):
        if self.species=="Fugu":
            return self.weight*5000
        elif self.species=="Koi":
            return self.weight*3000
        elif self.species=="Tai":
            return self.weight*4000
        else:
            return self.weight*2000
    def is_expensive(self): return self.calculate_price()>10000
    def __str__(self):
        return f"{self.name} ({self.species}): {self.weight} kg, {self.habitat}"

def process_fish_list(fish_list):
    total_weight=0
    total_price=0
    for f in fish_list:
        total_weight+=f.weight
        price=f.calculate_price()
        total_price+=price
        print(f"{f.name}: {price} yen")
    return [total_weight,total_price]

# Create some fish
fish1=fish("Bubbles",1.2,"Koi","freshwater")
fish2=fish("Spike",2.5,"Fugu","saltwater")
fish3=fish("Goldie",3.7,"Tai","saltwater")
fish_list=[fish1,fish2,fish3]

# Process the fish
results=process_fish_list(fish_list)
print(f"Total weight: {results[0]} kg")
print(f"Total price: {results[1]} yen")
```

2. Write a docstring for the `Fish` class and its methods following PEP 8 guidelines.

3. Rewrite the `process_fish_list` function to use better variable names and add appropriate comments.

### Exercise 2: Import Organization
1. The following code has poorly organized imports. Reorganize them according to PEP 8 guidelines:

```python
import matplotlib.pyplot as plt
import fish_database
from fish_utils import calculate_weight
import os
import sys
from datetime import datetime, timedelta
import numpy as np
import pandas as pd
from fish_analysis import analyze_data
import json
import csv
```

2. Create a Python script that imports modules from the standard library, third-party libraries, and local modules, organizing them according to PEP 8 guidelines.

### Exercise 3: Naming Conventions
1. Identify and fix the naming convention issues in the following code:

```python
def CalculateFishWeight(Length, Species):
    WEIGHT_FACTOR = 0.8
    if Species == "Koi":
        return Length * WEIGHT_FACTOR
    else:
        return Length * 0.5

class fishDatabase:
    def __init__(self):
        self.FISH_LIST = []
    
    def ADD_FISH(self, fish):
        self.FISH_LIST.append(fish)
    
    def get_Fish_By_Species(self, Species):
        return [f for f in self.FISH_LIST if f.species == Species]

MAX_fish_weight = 100
min_fish_weight = 0.1
```

2. Create a Python module with properly named variables, functions, classes, and constants related to fish data processing.

### Exercise 4: Code Style Analysis
1. Install and use a linter (e.g., `pycodestyle`, `flake8`, or `pylint`) to check the style of a Python file you've created.

2. Create a Python script that intentionally violates several PEP 8 guidelines, then use a linter to identify the issues.

3. Use the `black` formatter to automatically format your code according to PEP 8 guidelines.

## Working with .py Files

### Exercise 1: Creating Modules
1. Create a module called `fish_utils.py` with the following functions:
   - `calculate_weight(length, species)`: Calculate the weight of a fish based on its length and species.
   - `calculate_price(weight, species)`: Calculate the price of a fish based on its weight and species.
   - `is_freshwater(species)`: Return True if the species is a freshwater fish, False otherwise.

2. Create a script that imports and uses the functions from your module.

3. Add appropriate docstrings, comments, and error handling to your module.

### Exercise 2: Creating Packages
1. Create a package called `fish_analysis` with the following structure:
   ```
   fish_analysis/
   ├── __init__.py
   ├── core.py
   ├── utils.py
   └── visualization.py
   ```

2. Implement the following functionality:
   - `core.py`: Basic fish data processing functions
   - `utils.py`: Utility functions for file I/O and data conversion
   - `visualization.py`: Functions for plotting fish data

3. Make sure the package is properly importable and the functions are accessible.

### Exercise 3: Module Documentation
1. Add comprehensive docstrings to all functions and classes in your modules.

2. Generate documentation for your modules using a tool like `pydoc` or `Sphinx`.

3. Create a README file that explains how to use your modules and packages.

## Understanding main() and __name__

### Exercise 1: Script vs. Module
1. Create a Python file that can be used both as a script and as a module:
   - When run as a script, it should process fish data from a file specified as a command-line argument.
   - When imported as a module, it should provide functions for processing fish data.

2. Use the `if __name__ == "__main__":` pattern to separate script behavior from module behavior.

3. Test your file both by running it directly and by importing it from another script.

### Exercise 2: Main Function Organization
1. Create a complex script that processes fish data, but organize all the script logic into functions, with a `main()` function that orchestrates the process.

2. Make sure your script handles errors gracefully and provides helpful error messages.

3. Add logging to your script to track its execution.

### Exercise 3: Module Testing
1. Create a module with several functions for fish data processing.

2. Add a section at the end of the module that tests the functions when the module is run directly.

3. Make sure the tests don't run when the module is imported.

## Command Line Arguments

### Exercise 1: Basic Argument Handling
1. Create a script that takes the following command-line arguments:
   - A file path to a CSV file containing fish data
   - A species filter (optional)
   - An output file path (optional)

2. The script should read the fish data, filter it by species if specified, and write the results to the output file or print them to the console.

3. Use `sys.argv` to handle the command-line arguments.

### Exercise 2: Argparse Usage
1. Rewrite the script from Exercise 1 using `argparse` to handle command-line arguments.

2. Add the following features:
   - Help messages for each argument
   - Type checking for numeric arguments
   - Default values for optional arguments
   - Mutually exclusive argument groups

3. Add a `--verbose` flag that enables detailed output.

### Exercise 3: Command-Line Interface
1. Create a command-line interface for a fish database with the following subcommands:
   - `add`: Add a fish to the database
   - `list`: List all fish in the database
   - `search`: Search for fish by various criteria
   - `export`: Export the database to a file

2. Use `argparse` with subparsers to implement the subcommands.

3. Implement appropriate argument handling for each subcommand.

## Project Structure and Organization

### Exercise 1: Project Setup
1. Create a new Python project with the following structure:
   ```
   fish_project/
   ├── README.md
   ├── setup.py
   ├── requirements.txt
   ├── fish_project/
   │   ├── __init__.py
   │   ├── core.py
   │   ├── utils.py
   │   └── cli.py
   ├── tests/
   │   ├── __init__.py
   │   ├── test_core.py
   │   └── test_utils.py
   └── examples/
       └── basic_usage.py
   ```

2. Implement a simple fish data processing library in the project.

3. Write tests for your library using a testing framework like `pytest`.

### Exercise 2: Package Configuration
1. Create a `setup.py` file for your project that:
   - Specifies the package name, version, and description
   - Lists dependencies
   - Includes author information and license
   - Configures entry points for command-line scripts

2. Create a `requirements.txt` file that lists all the dependencies.

3. Make your package installable with `pip install -e .`.

### Exercise 3: Project Documentation
1. Create comprehensive documentation for your project, including:
   - A README file with installation and usage instructions
   - API documentation for all modules, classes, and functions
   - Examples of how to use your library

2. Set up a documentation generation system using Sphinx.

3. Create a simple website for your project documentation.

## Combined Exercises

### Exercise 1: Fish Database System
Create a complete fish database system with the following features:

1. A well-organized package structure following best practices
2. PEP 8 compliant code throughout
3. Comprehensive documentation
4. Command-line interface for interacting with the database
5. Functions for importing and exporting data
6. Data visualization capabilities
7. Unit tests for all functionality

### Exercise 2: Fish Data Analysis Tool
Create a data analysis tool for fish data with the following features:

1. Ability to read data from various file formats (CSV, JSON, Excel)
2. Statistical analysis functions
3. Data visualization functions
4. Command-line interface with rich argument handling
5. Well-structured project organization
6. Comprehensive documentation
7. Unit tests for all functionality

### Exercise 3: Fish Monitoring System
Create a simulated fish monitoring system with the following features:

1. A module for generating simulated fish data
2. A module for analyzing the data
3. A module for visualizing the data
4. A command-line interface for controlling the system
5. A well-organized project structure
6. Comprehensive documentation
7. Unit tests for all functionality

## Submission Guidelines
1. Submit your solutions as Python scripts or packages.
2. Include a README file explaining how to use your code.
3. Make sure your code follows PEP 8 guidelines.
4. Include tests for your code.
5. Document your code with appropriate docstrings and comments.

## Bonus Challenge
Create a complete Python project that demonstrates all the best practices covered in this section:
- PEP 8 compliant code
- Well-organized modules and packages
- Proper use of `if __name__ == "__main__":`
- Sophisticated command-line argument handling
- Comprehensive project structure
- Thorough documentation
- Extensive test coverage

The project should implement a fish inventory and analysis system that can be used both as a library and as a command-line tool.

Good luck!
