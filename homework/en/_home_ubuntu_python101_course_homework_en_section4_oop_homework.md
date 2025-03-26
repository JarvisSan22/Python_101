# Section 4: Object-Oriented Programming - Homework Assignments

## Assignment 1: Classes and Objects

### Part A: Basic Class Creation
1. Create a class called `JapaneseFish` with the following attributes:
   - `name`: The name of the fish
   - `species`: The species of the fish
   - `weight`: The weight of the fish in kilograms
   - `habitat`: The habitat of the fish (freshwater or saltwater)

2. Add the following methods to your `JapaneseFish` class:
   - `swim()`: Returns a string saying the fish is swimming
   - `feed(amount)`: Increases the fish's weight by 10% of the food amount
   - `describe()`: Returns a formatted string with all the fish's information

3. Create at least three instances of your `JapaneseFish` class with different Japanese fish (e.g., Koi, Fugu, Tai) and demonstrate all methods.

4. Add a class attribute `count` that keeps track of how many fish have been created. Update this in the `__init__` method.

### Part B: Properties and Encapsulation
1. Modify your `JapaneseFish` class to use a protected attribute `_weight` instead of `weight`.

2. Add a property `weight` with getter and setter methods that:
   - Getter: Returns the current weight
   - Setter: Validates that the weight is positive before setting it

3. Add a read-only property `weight_in_pounds` that converts the weight from kilograms to pounds (1 kg = 2.20462 lb).

4. Demonstrate the use of these properties by:
   - Creating a fish with a valid weight
   - Trying to set an invalid weight (should raise an error)
   - Displaying the weight in both kilograms and pounds

### Part C: Magic Methods
1. Add the following magic methods to your `JapaneseFish` class:
   - `__str__`: Returns a string representation of the fish
   - `__repr__`: Returns a string that could be used to recreate the fish object
   - `__lt__`: Compares fish based on their weights
   - `__eq__`: Checks if two fish are the same (same name and species)
   - `__add__`: Adds the weights of two fish or a fish and a number

2. Demonstrate each of these magic methods with appropriate examples.

## Assignment 2: Inheritance and Polymorphism

### Part A: Basic Inheritance
1. Create a base class `Aquatic` with:
   - Attributes: `name` and `habitat`
   - Methods: `swim()` and `breathe()`

2. Create a derived class `Fish` that inherits from `Aquatic` and adds:
   - Additional attributes: `species` and `weight`
   - Additional method: `feed(amount)`
   - Override the `breathe()` method to be specific to fish

3. Create at least two instances of your `Fish` class and demonstrate inheritance by calling both the inherited and new methods.

### Part B: Multiple Inheritance
1. Create a class `Edible` with:
   - Attributes: `taste` and `preparation`
   - Method: `cook()` that returns how the food should be prepared

2. Create a class `EdibleFish` that inherits from both `Aquatic` and `Edible` with:
   - Additional attribute: `price`
   - Method: `market_description()` that combines information from both parent classes

3. Create at least two instances of `EdibleFish` with different Japanese fish and demonstrate multiple inheritance.

### Part C: Abstract Base Classes
1. Convert your `Aquatic` class to an abstract base class with:
   - Abstract method: `breathe()`
   - Regular method: `swim()`

2. Create two concrete classes that inherit from `Aquatic`:
   - `FreshwaterFish`: Implements `breathe()` for freshwater fish
   - `SaltwaterFish`: Implements `breathe()` for saltwater fish

3. Try to instantiate the abstract base class (should fail) and then create instances of both concrete classes.

### Part D: Composition
1. Create a class `FishTank` that uses composition instead of inheritance:
   - Attributes: `length`, `width`, `height`, `volume` (calculated), and a list of `fish`
   - Methods: `add_fish(fish)`, `remove_fish(fish)`, `list_fish()`, and `total_weight()`

2. Create several `JapaneseFish` instances and add them to a `FishTank` instance.

3. Demonstrate the composition relationship by calling all the methods of `FishTank`.

## Assignment 3: Exception Handling

### Part A: Basic Exception Handling
1. Write a function `get_fish_weight(fish_data, fish_name)` that:
   - Takes a dictionary of fish data and a fish name
   - Returns the weight of the specified fish
   - Handles `KeyError` if the fish is not in the dictionary
   - Handles `TypeError` if the fish_data is not a dictionary

2. Test your function with:
   - Valid input
   - A fish name that's not in the dictionary
   - A non-dictionary input for fish_data

### Part B: Custom Exceptions
1. Create a custom exception hierarchy:
   - Base exception: `FishTankError`
   - Derived exceptions: `TankOvercrowdedError` and `InvalidFishError`

2. Write a function `add_fish_to_tank(tank_volume, fish_count, fish_size, fish_type)` that:
   - Raises `InvalidFishError` if the fish type is not allowed
   - Raises `TankOvercrowdedError` if the tank would be overcrowded
   - Returns a success message if the fish can be added

3. Test your function with various inputs to trigger both exceptions and the success case.

### Part C: Context Managers
1. Create a context manager class `FishMarket` that:
   - Opens the market in `__enter__`
   - Closes the market in `__exit__`
   - Has methods to `buy_fish(name, price)` and `sell_fish(name, price)`
   - Keeps track of inventory and profits

2. Use your context manager in a `with` statement to simulate a day at the fish market.

3. Demonstrate error handling within the context manager by trying to sell a fish that's not in inventory.

## Assignment 4: Practical Application

### Fish Inventory Management System

Create a complete fish inventory management system with the following components:

1. A `Fish` class hierarchy:
   - Base class: `Fish` with common attributes and methods
   - Derived classes: `FreshwaterFish` and `SaltwaterFish` with specific behaviors

2. A `FishTank` class that can contain multiple fish and manages:
   - Adding and removing fish
   - Feeding all fish
   - Calculating total weight
   - Checking if the tank is overcrowded

3. A `FishInventory` class that:
   - Loads and saves fish data from/to a file
   - Adds and removes fish from the inventory
   - Searches for fish by name or species
   - Generates reports on the inventory

4. Custom exceptions for error handling:
   - `InventoryError` as the base exception
   - Specific derived exceptions for different error types

5. A command-line interface that allows users to:
   - View all fish in the inventory
   - Add new fish
   - Remove fish
   - Search for fish
   - Generate reports
   - Save and load the inventory

Your implementation should demonstrate:
- Proper class design and inheritance
- Encapsulation and properties
- Exception handling
- File I/O with context managers
- Command-line interface using `argparse`

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
