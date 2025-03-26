# Section 1: Python Fundamentals - Homework Assignments

## Assignment 1: Python Basics

### Part A: Variables and Data Types
1. Create variables for the following Japanese fish and their characteristics:
   - A Koi fish that is 3 years old, weighs 2.5 kg, and has red and white coloration
   - A Fugu (pufferfish) that is 2 years old, weighs 1.8 kg, and is potentially poisonous
   - A Maguro (tuna) that weighs 80 kg and is used for sashimi

2. Print each fish's information using formatted strings (f-strings).

3. Calculate and print the total weight of all three fish.

4. Convert the weight of the Koi fish to grams and print the result.

### Part B: Operators and Expressions
1. Create variables for the length and width of a rectangular fish pond in meters.
2. Calculate and print the area and perimeter of the pond.
3. If the pond is 1.5 meters deep, calculate and print its volume in cubic meters.
4. A Koi fish needs at least 250 liters of water. Calculate and print how many Koi fish the pond can support.

### Part C: Conditional Statements
Write a program that:
1. Asks the user to input a fish name.
2. Checks if the fish is one of: "Koi", "Fugu", "Tai", "Maguro", or "Unagi".
3. For each fish, print specific information:
   - Koi: "Ornamental fish often kept in garden ponds"
   - Fugu: "Pufferfish that must be prepared by licensed chefs"
   - Tai: "Sea bream, often served on celebratory occasions"
   - Maguro: "Tuna, commonly used in sushi and sashimi"
   - Unagi: "Freshwater eel, typically served grilled with a sweet sauce"
4. If the fish is not in the list, print "Information not available for this fish".

### Part D: Loops
1. Create a list of 7 different Japanese fish.
2. Use a for loop to print each fish name and its length (number of characters).
3. Use a while loop to remove fish from the list one by one until only 3 remain, printing the removed fish and the current list after each removal.
4. Create a nested loop that iterates through 3 fish types and 3 cooking methods, printing all possible combinations.

## Assignment 2: Problem Solving with Python

### Problem 1: Fish Tank Temperature Monitoring
Write a program that:
1. Creates a list of hourly water temperature readings for a 24-hour period (you can make up the data).
2. Calculates and prints the average, minimum, and maximum temperatures.
3. Counts how many readings are outside the optimal range for Koi fish (18-24°C).
4. Prints a warning if any temperature reading is above 28°C or below 15°C.

### Problem 2: Fish Inventory System
Create a simple inventory system for a fish market:
1. Create variables for 5 different types of fish, each with a price per kilogram.
2. Ask the user to input the weight of each fish they want to buy.
3. Calculate and print the cost for each fish and the total cost.
4. Apply a 10% discount if the total cost is over 5000 yen.
5. Print the final amount to be paid.

### Problem 3: Fish Growth Tracker
Write a program that:
1. Starts with a young Koi fish that weighs 100 grams.
2. The fish grows 5% each month.
3. Use a loop to calculate and print the weight of the fish at the end of each month for 2 years (24 months).
4. After how many months will the fish weigh more than 500 grams?

### Problem 4: Fish Pond Simulation
Create a simple simulation of a fish pond:
1. Start with 10 fish in the pond.
2. Each month, the following events occur:
   - Each fish has a 10% chance of producing a new fish (reproduction).
   - Each fish has a 5% chance of being caught by a fisherman.
   - Each fish has a 2% chance of dying naturally.
3. Simulate the pond for 5 years (60 months) and print the fish population at the end of each year.
4. If the population exceeds 100 fish or drops to 0, end the simulation early.

## Submission Guidelines
1. Create a Python file for each assignment (assignment1.py and assignment2.py).
2. Include comments explaining your code.
3. Make sure your code is well-formatted and follows Python's PEP 8 style guide.
4. Test your code with different inputs to ensure it works correctly.
5. Submit your files by the deadline.

## Grading Criteria
- Correctness: Does the code produce the expected output? (40%)
- Completeness: Are all requirements implemented? (30%)
- Code quality: Is the code well-organized, commented, and following best practices? (20%)
- Creativity: Did you add any extra features or handle edge cases? (10%)
