# Section 2: Data Structures - Homework Assignments

## Assignment 1: Lists and Tuples

### Part A: List Operations
1. Create a list of at least 7 different Japanese fish.
2. Perform the following operations and print the list after each operation:
   - Add a new fish to the end of the list
   - Insert a fish at position 3
   - Remove a specific fish by name
   - Sort the list alphabetically
   - Reverse the list
   - Create a slice containing the first 3 fish
   - Create a slice containing the last 3 fish
3. Create a nested list where each inner list contains a fish name and its weight in kg. Then:
   - Print only the fish names
   - Print only the weights
   - Find and print the heaviest fish

### Part B: List Comprehensions
1. Using the list of Japanese fish, create a list comprehension that:
   - Creates a list of the lengths of each fish name
   - Creates a list of fish names that are longer than 4 characters
   - Creates a list of fish names in uppercase
   - Creates a list of tuples where each tuple contains a fish name and its length
2. Create a list of numbers from 1 to 20, then use list comprehensions to:
   - Create a list of squares of these numbers
   - Create a list of only the even numbers
   - Create a list of numbers divisible by both 2 and 3

### Part C: Tuples
1. Create a tuple containing information about a specific Japanese fish (name, weight, habitat, lifespan).
2. Demonstrate tuple unpacking to assign each value to a separate variable.
3. Try to modify an element of the tuple and explain what happens.
4. Create a list of tuples, where each tuple contains a fish name and its price. Then:
   - Sort the list by fish name
   - Sort the list by price
   - Find and print the most expensive fish

## Assignment 2: Sets and Dictionaries

### Part A: Set Operations
1. Create two sets:
   - A set of freshwater Japanese fish
   - A set of saltwater Japanese fish
2. Perform and explain the following set operations:
   - Union: all fish from both sets
   - Intersection: fish that can live in both freshwater and saltwater (if any)
   - Difference: fish that are exclusively freshwater
   - Symmetric difference: fish that are exclusively freshwater or exclusively saltwater
3. Create a set of endangered Japanese fish and:
   - Find endangered freshwater fish
   - Find endangered saltwater fish
   - Find non-endangered fish from both habitats

### Part B: Dictionary Operations
1. Create a dictionary representing a Japanese fish market, with fish names as keys and prices as values.
2. Implement the following operations:
   - Add new fish to the market
   - Update the price of an existing fish
   - Remove a fish from the market
   - Check if a specific fish is available
   - Print all available fish and their prices in a formatted way
3. Create a nested dictionary where:
   - The outer dictionary keys are fish categories (e.g., "Freshwater", "Saltwater")
   - The inner dictionaries contain fish names and their details (price, weight, etc.)
   - Demonstrate how to access, add, and modify information in this nested structure

### Part C: Dictionary Comprehensions
1. Using your fish market dictionary, create dictionary comprehensions that:
   - Create a dictionary of fish with prices above a certain threshold
   - Create a dictionary where the keys are fish names and the values are the length of each name
   - Create a dictionary with fish names as keys and their prices with a 10% discount as values
2. Given two lists (fish names and their weights), create a dictionary using dictionary comprehension.

## Assignment 3: String Operations and Formatting

### Part A: String Methods
1. Create a string variable containing a paragraph about Japanese fish.
2. Perform and explain the following string operations:
   - Convert to uppercase, lowercase, and title case
   - Count occurrences of a specific word
   - Replace all occurrences of one fish name with another
   - Split the paragraph into a list of sentences
   - Join a list of fish names into a single string with commas
3. Create a string with extra whitespace and demonstrate different ways to remove it.

### Part B: String Formatting
1. Create variables for a fish's name, type, weight, and price.
2. Format and print this information using:
   - %-formatting
   - str.format() method
   - f-strings
3. For each formatting method, include at least one number formatted to 2 decimal places.
4. Create a table-like output that displays information about multiple fish, properly aligned.

### Part C: Advanced String Operations
1. Create a function that takes a fish name and returns whether it's a palindrome (reads the same forward and backward).
2. Write a function that takes a sentence about fish and censors specific words by replacing them with asterisks.
3. Create a function that takes a fish name and returns all possible substrings of length 3 or more.
4. Implement a simple encryption/decryption function for fish names using a Caesar cipher (shifting letters).

## Assignment 4: Practical Applications

### Problem 1: Fish Inventory System
Create a program that:
1. Maintains an inventory of Japanese fish using a dictionary
2. Each fish has attributes: quantity, price per kg, and total value
3. Allows adding new fish, updating quantities, and removing fish
4. Calculates the total value of all fish in the inventory
5. Finds the most valuable fish in the inventory
6. Prints a formatted inventory report

### Problem 2: Fish Species Classifier
Create a program that:
1. Maintains sets of fish categorized by habitat (freshwater, saltwater, brackish)
2. Allows adding new fish to appropriate categories
3. Identifies fish that can live in multiple habitats
4. Provides functions to query which habitats a specific fish can live in
5. Prints a report showing the distribution of fish across different habitats

### Problem 3: Fish Market Analysis
Create a program that:
1. Stores daily prices of various Japanese fish over a week
2. Calculates and displays:
   - Average price for each fish
   - Price fluctuation (highest - lowest) for each fish
   - The day with the highest average price across all fish
   - The fish with the most stable price (least fluctuation)
3. Formats and prints a comprehensive price analysis report

### Problem 4: Fish Recipe Database
Create a program that:
1. Maintains a database of Japanese fish recipes using nested dictionaries
2. Each recipe includes ingredients, preparation time, cooking method, and difficulty level
3. Implements functions to:
   - Add new recipes
   - Search recipes by fish type
   - Filter recipes by cooking time or difficulty
   - Print a formatted recipe card for any selected recipe
4. Creates a recommendation system that suggests recipes based on available fish

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
