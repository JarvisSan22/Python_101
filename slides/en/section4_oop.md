# Section 4: Object-Oriented Programming

## Classes, Objects, and Inheritance

### Introduction to Object-Oriented Programming (OOP)
- A programming paradigm based on the concept of "objects"
- Objects contain data (attributes) and code (methods)
- Helps organize code, making it more reusable and maintainable
- Four main principles: Encapsulation, Abstraction, Inheritance, Polymorphism

### Classes and Objects
- A class is a blueprint for creating objects
- An object is an instance of a class
- Classes define attributes (data) and methods (functions)

```python
# Defining a simple class
class Fish:
    # Class attribute (shared by all instances)
    species_count = 0
    
    # Constructor method (initializes a new object)
    def __init__(self, name, species, weight):
        # Instance attributes (unique to each instance)
        self.name = name
        self.species = species
        self.weight = weight
        Fish.species_count += 1
    
    # Instance method
    def swim(self):
        return f"{self.name} is swimming!"
    
    # Instance method with parameters
    def feed(self, food_amount):
        self.weight += food_amount * 0.1
        return f"{self.name} has been fed {food_amount}g of food and now weighs {self.weight}kg."

# Creating objects (instances of the Fish class)
koi = Fish("Hanako", "Koi", 2.5)
fugu = Fish("Puff", "Fugu", 3.2)

# Accessing attributes
print(koi.name)  # "Hanako"
print(fugu.species)  # "Fugu"

# Calling methods
print(koi.swim())  # "Hanako is swimming!"
print(fugu.feed(50))  # "Puff has been fed 50g of food and now weighs 3.7kg."

# Accessing class attribute
print(f"Number of fish species: {Fish.species_count}")  # 2
```

### The `self` Parameter
- The first parameter of instance methods
- Refers to the instance itself
- Automatically passed when calling methods on an object
- Used to access instance attributes and methods

```python
class Fish:
    def __init__(self, name):
        self.name = name
    
    def identify(self):
        return f"I am {self.name}, a fish."
    
    def call_identify(self):
        # Using self to call another method
        return f"When asked who I am: {self.identify()}"

fish = Fish("Koi")
print(fish.identify())  # "I am Koi, a fish."
print(fish.call_identify())  # "When asked who I am: I am Koi, a fish."
```

### Class Methods and Static Methods
- Class methods operate on the class itself, not instances
- Static methods are related to the class but don't modify class or instance state

```python
class Fish:
    species_count = 0
    
    def __init__(self, name, species):
        self.name = name
        self.species = species
        Fish.species_count += 1
    
    # Instance method
    def swim(self):
        return f"{self.name} is swimming!"
    
    # Class method (operates on the class)
    @classmethod
    def get_species_count(cls):
        return f"There are {cls.species_count} fish species."
    
    # Static method (related to the class but doesn't modify class or instance state)
    @staticmethod
    def is_saltwater(species):
        saltwater_species = ["Tuna", "Fugu", "Tai"]
        return species in saltwater_species

# Creating objects
koi = Fish("Hanako", "Koi")
fugu = Fish("Puff", "Fugu")

# Calling instance method
print(koi.swim())  # "Hanako is swimming!"

# Calling class method
print(Fish.get_species_count())  # "There are 2 fish species."

# Calling static method
print(Fish.is_saltwater("Koi"))  # False
print(Fish.is_saltwater("Fugu"))  # True
```

### Properties and Encapsulation
- Encapsulation: Restricting direct access to some attributes
- Properties: Special methods that allow controlled access to attributes

```python
class Fish:
    def __init__(self, name, weight):
        self.name = name
        self._weight = weight  # Protected attribute (convention)
    
    # Getter property
    @property
    def weight(self):
        return self._weight
    
    # Setter property
    @weight.setter
    def weight(self, value):
        if value <= 0:
            raise ValueError("Weight must be positive")
        self._weight = value
    
    # Property with calculation
    @property
    def weight_in_pounds(self):
        return self._weight * 2.20462

fish = Fish("Koi", 2.5)
print(fish.weight)  # 2.5 (calls the getter)
fish.weight = 3.0  # Calls the setter
print(fish.weight)  # 3.0
print(fish.weight_in_pounds)  # 6.61386

try:
    fish.weight = -1  # Raises ValueError
except ValueError as e:
    print(f"Error: {e}")
```

### Magic Methods (Dunder Methods)
- Special methods with double underscores (e.g., `__init__`, `__str__`)
- Define behavior for built-in operations and functions

```python
class Fish:
    def __init__(self, name, species, weight):
        self.name = name
        self.species = species
        self.weight = weight
    
    # String representation (used by print() and str())
    def __str__(self):
        return f"{self.name} the {self.species} ({self.weight}kg)"
    
    # Representation (used by repr())
    def __repr__(self):
        return f"Fish('{self.name}', '{self.species}', {self.weight})"
    
    # Comparison (less than)
    def __lt__(self, other):
        return self.weight < other.weight
    
    # Addition (combining fish weights)
    def __add__(self, other):
        if isinstance(other, Fish):
            return self.weight + other.weight
        return self.weight + other

koi = Fish("Hanako", "Koi", 2.5)
fugu = Fish("Puff", "Fugu", 3.2)

print(koi)  # "Hanako the Koi (2.5kg)"
print(repr(koi))  # "Fish('Hanako', 'Koi', 2.5)"
print(koi < fugu)  # True (koi weighs less than fugu)
print(koi + fugu)  # 5.7 (sum of weights)
print(koi + 1.5)  # 4.0 (koi weight + 1.5)
```

---

### Inheritance
- Allows a class to inherit attributes and methods from another class
- Promotes code reuse and establishes a hierarchy

```python
# Base class (parent class)
class Aquatic:
    def __init__(self, name, habitat):
        self.name = name
        self.habitat = habitat
    
    def swim(self):
        return f"{self.name} is swimming in {self.habitat} water."
    
    def breathe(self):
        return f"{self.name} is breathing underwater."

# Derived class (child class)
class Fish(Aquatic):
    def __init__(self, name, habitat, species, weight):
        # Call the parent class's __init__ method
        super().__init__(name, habitat)
        self.species = species
        self.weight = weight
    
    def feed(self, food_amount):
        self.weight += food_amount * 0.1
        return f"{self.name} has been fed {food_amount}g of food."
    
    # Override the parent's breathe method
    def breathe(self):
        return f"{self.name} is breathing through gills."

# Creating objects
koi = Fish("Hanako", "fresh", "Koi", 2.5)

# Accessing attributes from the parent class
print(koi.name)  # "Hanako"
print(koi.habitat)  # "fresh"

# Calling methods from the parent class
print(koi.swim())  # "Hanako is swimming in fresh water."

# Calling methods from the child class
print(koi.feed(50))  # "Hanako has been fed 50g of food."

# Calling overridden method
print(koi.breathe())  # "Hanako is breathing through gills."
```

### Multiple Inheritance
- A class can inherit from multiple parent classes
- Allows combining features from different classes

```python
class Aquatic:
    def __init__(self, name, habitat):
        self.name = name
        self.habitat = habitat
    
    def swim(self):
        return f"{self.name} is swimming in {self.habitat} water."

class Edible:
    def __init__(self, taste, preparation):
        self.taste = taste
        self.preparation = preparation
    
    def cook(self):
        return f"{self.name if hasattr(self, 'name') else 'This'} is best {self.preparation}."

# Multiple inheritance
class EdibleFish(Aquatic, Edible):
    def __init__(self, name, habitat, taste, preparation, price):
        Aquatic.__init__(self, name, habitat)
        Edible.__init__(self, taste, preparation)
        self.price = price
    
    def market_description(self):
        return f"{self.name}: {self.taste} {self.habitat}water fish, {self.price} yen per kg."

# Creating an object
tai = EdibleFish("Tai", "salt", "mild and sweet", "grilled", 2500)

# Accessing attributes and methods from all parent classes
print(tai.name)  # "Tai"
print(tai.habitat)  # "salt"
print(tai.taste)  # "mild and sweet"
print(tai.swim())  # "Tai is swimming in salt water."
print(tai.cook())  # "Tai is best grilled."
print(tai.market_description())  # "Tai: mild and sweet saltwater fish, 2500 yen per kg."
```

### Method Resolution Order (MRO)
- The order in which Python looks for methods in a hierarchy of classes
- Important in multiple inheritance to determine which method is called

```python
class A:
    def method(self):
        return "Method from A"

class B(A):
    def method(self):
        return "Method from B"

class C(A):
    def method(self):
        return "Method from C"

class D(B, C):
    pass

# Creating an object
d = D()

# Checking the Method Resolution Order
print(D.__mro__)  # (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)

# Calling the method
print(d.method())  # "Method from B" (B comes before C in the MRO)
```

### Abstract Base Classes
- Define a common interface for derived classes
- Can't be instantiated directly
- Require derived classes to implement certain methods

```python
from abc import ABC, abstractmethod

class Aquatic(ABC):
    def __init__(self, name, habitat):
        self.name = name
        self.habitat = habitat
    
    def swim(self):
        return f"{self.name} is swimming in {self.habitat} water."
    
    @abstractmethod
    def breathe(self):
        pass  # This method must be implemented by derived classes

class Fish(Aquatic):
    def __init__(self, name, habitat, species):
        super().__init__(name, habitat)
        self.species = species
    
    # Implementing the abstract method
    def breathe(self):
        return f"{self.name} is breathing through gills."

class Mammal(Aquatic):
    def __init__(self, name, habitat, species):
        super().__init__(name, habitat)
        self.species = species
    
    # Implementing the abstract method
    def breathe(self):
        return f"{self.name} is breathing air and holding breath underwater."

# This would raise an error because Aquatic is abstract
# aquatic = Aquatic("Generic", "any")

# These are fine because they implement the abstract method
fish = Fish("Koi", "fresh", "Cyprinus carpio")
dolphin = Mammal("Flipper", "salt", "Tursiops truncatus")

print(fish.breathe())  # "Koi is breathing through gills."
print(dolphin.breathe())  # "Flipper is breathing air and holding breath underwater."
```

### Composition vs. Inheritance
- Inheritance: "is-a" relationship (a Koi is a Fish)
- Composition: "has-a" relationship (a FishTank has Fish)
- Composition often provides more flexibility than inheritance

```python
# Composition example
class Fish:
    def __init__(self, name, species, weight):
        self.name = name
        self.species = species
        self.weight = weight
    
    def swim(self):
        return f"{self.name} is swimming!"

class FishTank:
    def __init__(self, length, width, height):
        self.length = length
        self.width = width
        self.height = height
        self.volume = (length * width * height) / 1000  # liters
        self.fish = []  # Composition: FishTank has Fish
    
    def add_fish(self, fish):
        self.fish.append(fish)
        return f"{fish.name} added to the tank."
    
    def list_fish(self):
        if not self.fish:
            return "The tank is empty."
        fish_list = [f.name for f in self.fish]
        return f"Fish in the tank: {', '.join(fish_list)}"
    
    def total_weight(self):
        return sum(f.weight for f in self.fish)

# Creating objects
koi = Fish("Hanako", "Koi", 2.5)
fugu = Fish("Puff", "Fugu", 3.2)
tank = FishTank(100, 40, 30)

# Using composition
print(tank.add_fish(koi))  # "Hanako added to the tank."
print(tank.add_fish(fugu))  # "Puff added to the tank."
print(tank.list_fish())  # "Fish in the tank: Hanako, Puff"
print(f"Total fish weight: {tank.total_weight()} kg")  # "Total fish weight: 5.7 kg"
```

## Exception Handling

### Introduction to Exceptions
- Exceptions are events that disrupt the normal flow of a program
- Python uses try/except blocks to handle exceptions
- Proper exception handling makes programs more robust

### Try/Except Blocks
```python
# Basic try/except
try:
    fish_count = int(input("Enter number of fish: "))
    print(f"You have {fish_count} fish.")
except ValueError:
    print("That's not a valid number!")

# Handling specific exceptions
try:
    fish_data = {"Koi": 2.5, "Fugu": 3.2}
    fish_name = input("Enter fish name: ")
    weight = fish_data[fish_name]
    print(f"{fish_name} weighs {weight} kg.")
except KeyError:
    print(f"Sorry, {fish_name} is not in our database.")
except Exception as e:
    print(f"An error occurred: {e}")
```

### Try/Except/Else/Finally
```python
try:
    fish_file = open("fish_data.txt", "r")
    fish_count = int(fish_file.readline())
except FileNotFoundError:
    print("Fish data file not found.")
    fish_count = 0
except ValueError:
    print("Fish data file contains invalid data.")
    fish_count = 0
else:
    # This runs if no exceptions were raised
    print(f"Successfully read fish count: {fish_count}")
finally:
    # This always runs, regardless of whether an exception occurred
    if 'fish_file' in locals() and not fish_file.closed:
        fish_file.close()
        print("Fish data file closed.")
```

### Raising Exceptions
```python
def add_fish_to_tank(tank_volume, fish_count, fish_size):
    # Each fish needs at least 10 liters of water
    required_volume = fish_count * fish_size * 10
    
    if required_volume > tank_volume:
        raise ValueError(f"Tank too small! Needs {required_volume} liters, but only has {tank_volume} liters.")
    
    return f"{fish_count} fish added to the tank."

try:
    result = add_fish_to_tank(100, 15, 1.2)
    print(result)
except ValueError as e:
    print(f"Error: {e}")
```

### Creating Custom Exceptions
```python
class FishTankError(Exception):
    """Base class for fish tank exceptions."""
    pass

class TankOvercrowdedError(FishTankError):
    """Raised when the tank is overcrowded."""
    def __init__(self, tank_volume, required_volume):
        self.tank_volume = tank_volume
        self.required_volume = required_volume
        self.message = f"Tank overcrowded! Needs {required_volume} liters, but only has {tank_volume} liters."
        super().__init__(self.message)

class InvalidFishError(FishTankError):
    """Raised when an invalid fish is added to the tank."""
    pass

def add_fish_to_tank(tank_volume, fish_count, fish_size, fish_type):
    if fish_type not in ["Koi", "Goldfish", "Guppy", "Tetra"]:
        raise InvalidFishError(f"Cannot add {fish_type} to this tank.")
    
    required_volume = fish_count * fish_size * 10
    
    if required_volume > tank_volume:
        raise TankOvercrowdedError(tank_volume, required_volume)
    
    return f"{fish_count} {fish_type} added to the tank."

try:
    result = add_fish_to_tank(100, 5, 1.2, "Shark")
    print(result)
except InvalidFishError as e:
    print(f"Invalid fish error: {e}")
except TankOvercrowdedError as e:
    print(f"Overcrowding error: {e}")
except FishTankError as e:
    print(f"General fish tank error: {e}")
```

### Context Managers (with Statement)
```python
# Using a context manager for file operations
try:
    with open("fish_data.txt", "w") as file:
        file.write("Koi,2.5\n")
        file.write("Fugu,3.2\n")
        file.write("Tai,1.8\n")
    print("Fish data written successfully.")
except IOError as e:
    print(f"Error writing fish data: {e}")

# Creating a custom context manager
class FishTank:
    def __init__(self, name, volume):
        self.name =<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>