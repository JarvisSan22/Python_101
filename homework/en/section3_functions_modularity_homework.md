# Section 3: Functions and Modularity - Homework Assignments

## Assignment 1: Functions and Parameters

### Part A: Basic Functions
1. Write a function called `greet_fish` that takes a fish name as a parameter and prints a greeting to that fish.
2. Write a function called `calculate_tank_volume` that calculates the volume of a rectangular fish tank in liters. It should take length, width, and height (in centimeters) as parameters.
3. Write a function called `fish_info` that takes a fish name, weight, and habitat as parameters, with habitat defaulting to "freshwater". The function should print a formatted string with this information.
4. Write a function called `is_safe_to_eat` that takes a fish name and returns `True` if the fish is safe to eat raw (use a list of safe fish that includes "Tai", "Maguro", "Sake", "Hamachi", but not "Fugu").

### Part B: Return Values
1. Write a function called `convert_weight` that takes a weight in kilograms and a unit ("g", "kg", or "lb") and returns the converted weight.
2. Write a function called `fish_price_calculator` that takes the fish type, weight (in kg), and price per kg (defaulting to 1000 yen) and returns the total price.
3. Write a function called `analyze_fish_data` that takes a list of fish weights and returns a tuple containing the minimum, maximum, and average weights.
4. Write a function called `categorize_fish` that takes a fish name and returns whether it's "freshwater", "saltwater", or "unknown" based on a predefined dictionary of fish types.

### Part C: Variable Scope
1. Create a global variable called `total_fish_count` and initialize it to 0. Write a function called `add_fish` that takes a count parameter and correctly updates the global variable.
2. Write a function called `create_fish_counter` that initializes a local count variable to 0 and returns a nested function that increments and returns this count when called.
3. Explain the difference between local and global variables, and when you would use each.
4. Demonstrate how to modify a global list from within a function without using the `global` keyword.

### Part D: Lambda Functions
1. Write a lambda function that takes a fish name and returns its length.
2. Use the `sorted()` function with a lambda to sort a list of fish tuples (name, weight) by weight.
3. Use the `filter()` function with a lambda to filter a list of fish weights, keeping only those above 2 kg.
4. Use the `map()` function with a lambda to convert a list of fish weights in kg to pounds (1 kg = 2.20462 lb).

## Assignment 2: Modules and Imports

### Part A: Using Built-in Modules
1. Use the `random` module to:
   - Generate a random number between 1 and 100
   - Randomly select 3 fish from a list of at least 8 fish
   - Shuffle a list of fish
   - Generate a random float between 0 and 1, then scale it to represent a fish weight between 0.5 and 5 kg

2. Use the `datetime` module to:
   - Print the current date and time
   - Calculate and print the date 30 days from now
   - Calculate the number of days between two dates
   - Format a date as "YYYY-MM-DD"

3. Use the `math` module to:
   - Calculate the area of a circular fish pond with a given radius
   - Round a fish weight to the nearest 0.5 kg
   - Calculate the volume of a cylindrical fish tank

4. Use the `os` and `os.path` modules to:
   - Get the current working directory
   - Check if a file exists
   - Get the size of a file
   - Join directory and file names to create a path

### Part B: Creating Your Own Module
1. Create a module called `fish_utils.py` with the following functions:
   - `calculate_tank_volume(length, width, height)`: Calculate the volume of a rectangular tank in liters
   - `is_tank_overcrowded(tank_volume, fish_count, liters_per_fish=10)`: Check if a tank is overcrowded
   - `recommend_fish_count(tank_volume, liters_per_fish=10)`: Recommend the maximum number of fish for a tank
   - `convert_temperature(temp, from_unit, to_unit)`: Convert temperature between Celsius and Fahrenheit

2. Create a separate Python script that imports and uses your module to:
   - Calculate the volume of a tank with dimensions 100cm × 40cm × 30cm
   - Check if the tank is overcrowded with 15 fish
   - Get the recommended fish count for the tank
   - Convert 25°C to Fahrenheit

3. Add appropriate docstrings to all functions in your module.

4. Add a `if __name__ == "__main__":` block to your module that demonstrates its functionality when run directly.

## Assignment 3: File Input/Output Operations

### Part A: Basic File Operations
1. Write a program that:
   - Creates a file called "japanese_fish.txt"
   - Writes at least 8 Japanese fish names to the file, one per line
   - Closes the file
   - Opens the file again and reads its contents
   - Prints each fish name with its length (number of characters)

2. Modify the program to:
   - Ask the user for a fish name
   - Append the fish name to the file
   - Read and print the updated file contents

3. Write a program that:
   - Opens a text file
   - Counts the number of lines, words, and characters in the file
   - Prints the results

4. Write a program that:
   - Reads a file containing fish names
   - Creates a new file that contains only the fish names starting with a specific letter
   - Prints how many fish were copied to the new file

### Part B: CSV and JSON Files
1. Create a CSV file containing information about at least 5 Japanese fish, including:
   - Name
   - Type (freshwater/saltwater)
   - Average weight (kg)
   - Price per kg (yen)

2. Write a program that:
   - Reads the CSV file
   - Calculates the total value of each fish for a given weight
   - Writes the results to a new CSV file

3. Create a JSON file representing a fish database with at least 5 fish. Each fish should have:
   - Name
   - Scientific name
   - Habitat
   - Average size
   - Edible (boolean)
   - Colors (list)

4. Write a program that:
   - Reads the JSON file
   - Allows the user to search for a fish by name
   - Displays all information about the found fish
   - Handles the case where the fish is not found

### Part C: File System Operations
1. Write a program that:
   - Creates a directory called "fish_data"
   - Creates subdirectories for "freshwater" and "saltwater"
   - Creates a text file in each subdirectory with appropriate fish names
   - Lists all files and directories created

2. Write a program that:
   - Recursively walks through a directory
   - Finds all .txt files
   - Prints the total number of lines across all text files

3. Write a program that:
   - Monitors a directory for changes
   - When a new .txt file is added, reads its contents and counts the number of fish names
   - Prints the results

4. Write a program that:
   - Takes a directory path as input
   - Creates a backup of all .txt files in that directory
   - Adds a timestamp to the backup file names

## Assignment 4: Practical Applications

### Problem 1: Fish Database Manager
Create a program that manages a database of Japanese fish. The program should:
1. Load fish data from a JSON file
2. Provide functions to:
   - Add a new fish with details
   - Update existing fish information
   - Delete a fish
   - Search for fish by name or characteristics
3. Save the updated data back to the JSON file
4. Include error handling for file operations and user input
5. Use functions with appropriate parameters and return values
6. Include docstrings for all functions

### Problem 2: Fish Tank Simulator
Create a program that simulates a fish tank environment. The program should:
1. Define classes for Fish and Tank
2. Allow adding and removing fish from the tank
3. Track water quality parameters (temperature, pH, ammonia levels)
4. Simulate the passage of time and its effects on the tank
5. Save and load the tank state from a file
6. Provide recommendations for tank maintenance
7. Use appropriate modules for random events and time tracking

### Problem 3: Fish Market Inventory System
Create a program that manages inventory for a fish market. The program should:
1. Track stock levels, prices, and sales of different fish
2. Read initial inventory from a CSV file
3. Provide functions to:
   - Update stock when new fish arrive
   - Process sales and update inventory
   - Generate reports on current stock and sales
4. Save updated inventory to the CSV file
5. Include a command-line interface using `argparse`
6. Implement the program in a modular way with a main function

### Problem 4: Fish Recipe Finder
Create a program that helps users find recipes based on available fish. The program should:
1. Load a database of recipes from a JSON file
2. Allow users to input which fish they have
3. Search for and recommend recipes that use those fish
4. Filter recipes based on preparation time or difficulty
5. Save favorite recipes to a separate file
6. Include functions for all major operations
7. Use appropriate error handling
8. Implement a simple command-line interface

## Submission Guidelines
1. Create separate Python files for each assignment (assignment1.py, assignment2.py, etc.).
2. Include comments explaining your code.
3. Make sure your code is well-formatted and follows Python's PEP 8 style guide.
4. Test your code with different inputs to ensure it works correctly.
5. Submit your files by the deadline.

## Grading Criteria
- Correctness: Does the code produce the expected output? (40%)
- Completeness: Are all requirements implemented? (30%)
- Code quality: Is the code well-organized, commented, and following best practices? (20%)
- Creativity: Did you add any extra features or handle edge cases? (10%)
