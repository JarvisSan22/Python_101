# Python Classes and Objects: Building Your Own Fish Types

*A conversation between Kurumi and Jarvis*

![Kurumi and Jarvis](../../assets/images/kurumi_jarvis_placeholder.jpg)

## Introduction to Object-Oriented Programming

**Kurumi**: Jarvis, I've been writing Python code for a while now, but I keep hearing about something called "object-oriented programming." What exactly is that?

**Jarvis**: Great question, Kurumi! Object-oriented programming, or OOP for short, is a programming paradigm that organizes code around "objects" rather than functions and logic.

**Kurumi**: Objects? Like physical objects?

**Jarvis**: Think of objects as digital representations of things that might exist in the real world or in our program's world. For example, if we were building a fish database, we might have objects representing different fish, each with its own characteristics and behaviors.

**Kurumi**: That makes sense! So instead of having separate variables for each fish's name, weight, and species, we could group them together?

**Jarvis**: Exactly! And not just group data together, but also the functions that operate on that data. This approach helps organize code, makes it more reusable, and often maps better to how we think about the real world.

## Classes and Objects

**Kurumi**: So how do we create these objects in Python?

**Jarvis**: In Python, we define a blueprint called a "class," and then create "objects" (also called "instances") from that blueprint. Let me show you:

```python
# Defining a class (blueprint)
class Fish:
    def __init__(self, name, species, weight):
        self.name = name
        self.species = species
        self.weight = weight
    
    def swim(self):
        return f"{self.name} is swimming!"

# Creating objects (instances)
koi = Fish("Hanako", "Koi", 2.5)
fugu = Fish("Puff", "Fugu", 3.2)

# Using the objects
print(koi.name)  # Output: Hanako
print(fugu.species)  # Output: Fugu
print(koi.swim())  # Output: Hanako is swimming!
```

**Kurumi**: I see! So `Fish` is the class, and `koi` and `fugu` are objects created from that class. What's that `__init__` function doing?

**Jarvis**: The `__init__` method is a special method called a constructor. It's automatically called when you create a new object from the class. It initializes the object's attributes. The `self` parameter refers to the object being created.

**Kurumi**: And what about that `self` parameter in the methods? Why do we need that?

**Jarvis**: The `self` parameter is how methods access the object they belong to. When you call `koi.swim()`, Python automatically passes `koi` as the `self` parameter to the `swim` method. This allows the method to access the object's attributes, like `self.name`.

**Kurumi**: That's clever! So each object has its own copy of the attributes, but they share the methods?

**Jarvis**: Exactly! Each `Fish` object has its own name, species, and weight, but they all use the same `swim` method. This is efficient because the method code is stored only once, regardless of how many fish objects you create.

## Attributes and Methods

**Kurumi**: So attributes are the data, and methods are the functions that belong to a class?

**Jarvis**: That's right! Let's expand our `Fish` class with more attributes and methods:

```python
class Fish:
    # Class attribute (shared by all instances)
    species_count = 0
    
    def __init__(self, name, species, weight, habitat="freshwater"):
        # Instance attributes (unique to each instance)
        self.name = name
        self.species = species
        self.weight = weight
        self.habitat = habitat
        Fish.species_count += 1
    
    # Instance methods
    def swim(self):
        return f"{self.name} is swimming in {self.habitat} water!"
    
    def feed(self, food_amount):
        self.weight += food_amount * 0.1
        return f"{self.name} has been fed {food_amount}g of food and now weighs {self.weight}kg."
    
    def describe(self):
        return f"{self.name} is a {self.species} weighing {self.weight}kg that lives in {self.habitat} water."
    
    # Class method
    @classmethod
    def get_species_count(cls):
        return f"There are {cls.species_count} fish species."
```

**Kurumi**: I notice you have something called a "class attribute" and a "class method." How are those different from the instance ones?

**Jarvis**: Great observation! Class attributes are shared by all instances of the class, while instance attributes are unique to each instance. Similarly, class methods operate on the class itself rather than on instances.

**Kurumi**: So `species_count` keeps track of how many fish we've created?

**Jarvis**: Exactly! Let's see it in action:

```python
koi = Fish("Hanako", "Koi", 2.5)
fugu = Fish("Puff", "Fugu", 3.2, "saltwater")
tai = Fish("Tai", "Red Snapper", 1.8, "saltwater")

print(Fish.species_count)  # Output: 3
print(Fish.get_species_count())  # Output: There are 3 fish species.

print(koi.describe())  # Output: Hanako is a Koi weighing 2.5kg that lives in freshwater water.
print(fugu.describe())  # Output: Puff is a Fugu weighing 3.2kg that lives in saltwater water.

print(koi.feed(50))  # Output: Hanako has been fed 50g of food and now weighs 7.5kg.
```

**Kurumi**: I see! And I notice you added a default value for `habitat`. That's handy!

**Jarvis**: Yes, default parameter values work the same way in class methods as they do in regular functions. It's a convenient way to make some parameters optional.

## Encapsulation and Properties

**Kurumi**: In our `Fish` class, anyone can directly change the attributes, like `koi.weight = -10`. That doesn't seem right for a fish to have negative weight!

**Jarvis**: You've identified one of the key principles of OOP: encapsulation. Encapsulation means controlling access to the internal state of an object. In Python, we can use properties to achieve this:

```python
class Fish:
    def __init__(self, name, species, weight):
        self.name = name
        self.species = species
        self._weight = weight  # Protected attribute (convention)
    
    # Property for weight
    @property
    def weight(self):
        return self._weight
    
    @weight.setter
    def weight(self, value):
        if value <= 0:
            raise ValueError("Weight must be positive")
        self._weight = value
    
    # Read-only property
    @property
    def weight_in_pounds(self):
        return self._weight * 2.20462
```

**Kurumi**: So we use an underscore prefix to indicate that `_weight` is protected, and then provide controlled access through properties?

**Jarvis**: Exactly! The underscore is a convention in Python to indicate that an attribute is intended for internal use. Then we use properties to provide getter and setter methods that control how the attribute is accessed and modified.

**Kurumi**: Let's see how this works:

```python
koi = Fish("Hanako", "Koi", 2.5)
print(koi.weight)  # Output: 2.5 (calls the getter)

koi.weight = 3.0  # Calls the setter
print(koi.weight)  # Output: 3.0

print(koi.weight_in_pounds)  # Output: 6.61386 (calls the read-only property)

try:
    koi.weight = -1  # This will raise an error
except ValueError as e:
    print(f"Error: {e}")  # Output: Error: Weight must be positive
```

**Jarvis**: Perfect! Now we can ensure that a fish's weight is always positive. And we've provided a convenient way to get the weight in pounds without storing it separately.

**Kurumi**: What about private attributes that can't be accessed at all from outside the class?

**Jarvis**: In Python, there's no true private access modifier like in some other languages. However, there's a convention to use double underscores to make attributes name-mangled, which makes them harder (but not impossible) to access from outside:

```python
class Fish:
    def __init__(self, name):
        self.name = name
        self.__secret = "I can hold my breath for 10 minutes!"
    
    def reveal_secret(self):
        return self.__secret

koi = Fish("Hanako")
print(koi.name)  # Output: Hanako
# print(koi.__secret)  # This would raise an AttributeError
print(koi.reveal_secret())  # Output: I can hold my breath for 10 minutes!
```

**Kurumi**: So we can still access the secret through a method, but not directly?

**Jarvis**: That's right. It's a way of saying "this attribute is for internal use only." But remember, in Python, we follow the principle of "we're all consenting adults here" – meaning we trust developers to respect these conventions rather than enforcing strict access controls.

## Magic Methods (Dunder Methods)

**Kurumi**: I've noticed that `__init__` has double underscores. Are there other special methods like that?

**Jarvis**: Yes, those are called "magic methods" or "dunder methods" (for "double underscore"). They allow you to define how your objects behave with built-in Python operations. Let's add some to our `Fish` class:

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
```

**Kurumi**: So these methods define how our fish objects behave with different operations?

**Jarvis**: Exactly! Let's see them in action:

```python
koi = Fish("Hanako", "Koi", 2.5)
fugu = Fish("Puff", "Fugu", 3.2)

print(koi)  # Output: Hanako the Koi (2.5kg)
print(repr(koi))  # Output: Fish('Hanako', 'Koi', 2.5)

print(koi < fugu)  # Output: True (koi weighs less than fugu)
print(koi + fugu)  # Output: 5.7 (sum of weights)
print(koi + 1.5)  # Output: 4.0 (koi weight + 1.5)
```

**Kurumi**: That's really powerful! So we can make our objects work with Python's built-in operators and functions.

**Jarvis**: Yes, and there are many more magic methods for different operations:
- `__eq__`, `__ne__`, `__gt__`, `__ge__`, `__le__` for comparisons
- `__sub__`, `__mul__`, `__truediv__` for arithmetic
- `__len__`, `__getitem__`, `__setitem__` for container-like behavior
- And many more!

## Inheritance

**Kurumi**: What if I want to create different types of fish that share some common characteristics but also have their own unique features?

**Jarvis**: That's where inheritance comes in! Inheritance allows a class to inherit attributes and methods from another class. Let's see how it works:

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
```

**Kurumi**: So `Fish` inherits from `Aquatic` and gets all its methods and attributes?

**Jarvis**: Yes! The `Fish` class inherits the `swim` method from `Aquatic`, overrides the `breathe` method with its own implementation, and adds a new `feed` method. Let's see it in action:

```python
koi = Fish("Hanako", "fresh", "Koi", 2.5)

# Accessing attributes from the parent class
print(koi.name)  # Output: Hanako
print(koi.habitat)  # Output: fresh

# Calling methods from the parent class
print(koi.swim())  # Output: Hanako is swimming in fresh water.

# Calling methods from the child class
print(koi.feed(50))  # Output: Hanako has been fed 50g of food.

# Calling overridden method
print(koi.breathe())  # Output: Hanako is breathing through gills.
```

**Kurumi**: That's really useful! So we can create a hierarchy of classes, with more general classes at the top and more specific ones below.

**Jarvis**: Exactly! And Python even supports multiple inheritance, where a class can inherit from multiple parent classes:

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
```

**Kurumi**: So `EdibleFish` inherits from both `Aquatic` and `Edible`? That's powerful!

**Jarvis**: Yes, but use multiple inheritance carefully, as it can get complex. A common pattern is to use "mixins" – small, focused classes that provide specific functionality.

## Polymorphism

**Kurumi**: You mentioned that the `Fish` class overrides the `breathe` method from `Aquatic`. Is there a name for this ability to have different implementations of the same method?

**Jarvis**: Yes, that's called polymorphism! It allows objects of different classes to be treated as objects of a common superclass, but each can respond differently to the same method call:

```python
def describe_breathing(aquatic_creature):
    return aquatic_creature.breathe()

# Create different types of aquatic creatures
koi = Fish("Hanako", "fresh", "Koi", 2.5)
dolphin = Mammal("Flipper", "salt", "Bottlenose Dolphin")  # Assuming we have a Mammal class

# Same function, different behavior based on the object type
print(describe_breathing(koi))  # Output: Hanako is breathing through gills.
print(describe_breathing(dolphin))  # Output: Flipper is breathing air and holding breath underwater.
```

**Kurumi**: So the same function call behaves differently depending on the type of object it's called with?

**Jarvis**: Exactly! This is a powerful concept in OOP that allows for more flexible and extensible code. You can write code that works with a general type, and it will automatically work with all specific types derived from it.

## Abstract Base Classes

**Kurumi**: What if I want to create a base class that defines a common interface but doesn't provide implementations for all methods?

**Jarvis**: That's where abstract base classes come in! They allow you to define methods that must be implemented by derived classes:

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
 <response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>