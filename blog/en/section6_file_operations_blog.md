# Mastering File Operations and Exception Handling in Python

*A friendly conversation between Kurumi and Jarvis about working with files and handling errors in Python*

![Kurumi and Jarvis](../../assets/images/kurumi_jarvis.jpg)

## Introduction

**Kurumi**: *[looking frustrated at her laptop]* Jarvis, I'm trying to write a program that reads data from a file, but it keeps crashing when the file doesn't exist. There must be a better way to handle this!

**Jarvis**: *[nodding]* That's a common issue, Kurumi. What you're experiencing is related to two important Python concepts: file operations and exception handling.

**Kurumi**: *[curious]* Exception handling? Is that like dealing with errors?

**Jarvis**: Exactly! Exception handling is how your program responds when something unexpected happens. And file operations are often where exceptions occur because they involve external resources that might not be available or accessible.

**Kurumi**: That makes sense. I guess my program shouldn't just crash when a file is missing. It should handle that situation gracefully.

**Jarvis**: Precisely! Let's dive into both topics, starting with file operations, and then we'll see how to make them more robust with exception handling.

## Working with Files in Python

**Kurumi**: So how do I properly work with files in Python?

**Jarvis**: Python makes file operations quite straightforward. The basic pattern is: open the file, perform operations (read or write), and then close the file. Let me show you:

```python
# Basic file writing
file = open('fish_data.txt', 'w')  # 'w' means write mode
file.write("Koi: 1.2 kg, freshwater\n")
file.write("Fugu: 2.5 kg, saltwater\n")
file.close()  # Important: always close files when done

# Basic file reading
file = open('fish_data.txt', 'r')  # 'r' means read mode
content = file.read()
print(content)
file.close()
```

**Kurumi**: That seems simple enough. But I've heard there's a better way to open files that automatically handles closing them?

**Jarvis**: *[smiling]* You're thinking of the `with` statement, which is indeed the recommended approach. It's called a context manager, and it ensures the file is properly closed even if an error occurs:

```python
# Writing with a context manager
with open('fish_data.txt', 'w') as file:
    file.write("Koi: 1.2 kg, freshwater\n")
    file.write("Fugu: 2.5 kg, saltwater\n")
    # File is automatically closed when the block ends

# Reading with a context manager
with open('fish_data.txt', 'r') as file:
    content = file.read()
    print(content)
    # File is automatically closed when the block ends
```

**Kurumi**: That looks much cleaner! What are the different modes for opening files?

**Jarvis**: Great question! Here are the common file modes:

- `'r'` - Read (default)
- `'w'` - Write (creates a new file or truncates an existing one)
- `'a'` - Append (adds to the end of the file)
- `'b'` - Binary mode (e.g., 'rb', 'wb')
- `'t'` - Text mode (default)
- `'+'` - Read and write (e.g., 'r+')

**Kurumi**: *[thinking]* So if I want to add data to an existing file without erasing what's already there, I should use append mode?

**Jarvis**: Exactly! Let me show you:

```python
# Appending to a file
with open('fish_data.txt', 'a') as file:
    file.write("Tai: 3.7 kg, saltwater\n")
    file.write("Unagi: 1.8 kg, freshwater\n")
```

## Reading from Files

**Kurumi**: What are the different ways to read from a file?

**Jarvis**: There are several methods depending on what you need:

```python
# Reading the entire file at once
with open('fish_data.txt', 'r') as file:
    content = file.read()
    print(content)

# Reading line by line (memory efficient for large files)
with open('fish_data.txt', 'r') as file:
    for line in file:
        print(line.strip())  # strip() removes trailing newline

# Reading all lines into a list
with open('fish_data.txt', 'r') as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())

# Reading a specific number of characters
with open('fish_data.txt', 'r') as file:
    chunk = file.read(10)  # Read first 10 characters
    print(chunk)
```

**Kurumi**: *[excited]* This is really helpful! What if I want to process the data in the file? For example, if each line has information about a fish, how would I extract that?

**Jarvis**: You'd typically split each line into parts. Here's an example:

```python
with open('fish_data.txt', 'r') as file:
    for line in file:
        # Assuming format: "Species: weight kg, habitat"
        parts = line.strip().split(': ')
        species = parts[0]
        
        # Further split the second part
        weight_habitat = parts[1].split(', ')
        weight = weight_habitat[0]
        habitat = weight_habitat[1]
        
        print(f"Species: {species}, Weight: {weight}, Habitat: {habitat}")
```

**Kurumi**: *[nodding]* I see. But that seems a bit complex and error-prone. Are there better ways to work with structured data?

## Working with CSV and JSON Files

**Jarvis**: Absolutely! For structured data, Python provides modules for common formats like CSV and JSON. Let's start with CSV:

```python
import csv

# Writing CSV data
fish_data = [
    ['Species', 'Weight (kg)', 'Habitat'],
    ['Koi', 1.2, 'freshwater'],
    ['Fugu', 2.5, 'saltwater'],
    ['Tai', 3.7, 'saltwater'],
    ['Unagi', 1.8, 'freshwater'],
    ['Saba', 2.9, 'saltwater']
]

with open('fish_data.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerows(fish_data)

# Reading CSV data
with open('fish_data.csv', 'r', newline='') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

**Kurumi**: That's much cleaner! What about JSON? I've heard it's popular for web applications.

**Jarvis**: JSON is indeed very popular, especially for web APIs. Python's `json` module makes it easy to work with:

```python
import json

# Writing JSON data
fish_data = {
    'fish': [
        {'species': 'Koi', 'weight': 1.2, 'habitat': 'freshwater'},
        {'species': 'Fugu', 'weight': 2.5, 'habitat': 'saltwater'},
        {'species': 'Tai', 'weight': 3.7, 'habitat': 'saltwater'},
        {'species': 'Unagi', 'weight': 1.8, 'habitat': 'freshwater'},
        {'species': 'Saba', 'weight': 2.9, 'habitat': 'saltwater'}
    ]
}

with open('fish_data.json', 'w') as file:
    json.dump(fish_data, file, indent=4)

# Reading JSON data
with open('fish_data.json', 'r') as file:
    loaded_data = json.load(file)
    for fish in loaded_data['fish']:
        print(f"{fish['species']}: {fish['weight']} kg, {fish['habitat']}")
```

**Kurumi**: *[impressed]* That's really nice! The JSON format seems very intuitive.

**Jarvis**: It is! JSON is essentially a representation of Python dictionaries and lists, which makes it very natural to work with in Python.

## File System Operations

**Kurumi**: What about other file operations, like checking if a file exists or creating directories?

**Jarvis**: For those operations, you'll want to use the `os` and `shutil` modules:

```python
import os
import shutil

# Check if a file exists
if os.path.exists('fish_data.txt'):
    print('File exists')

# Get file information
if os.path.isfile('fish_data.txt'):
    print('It is a file')
    print(f"Size: {os.path.getsize('fish_data.txt')} bytes")
    print(f"Last modified: {os.path.getmtime('fish_data.txt')}")

# Directory operations
current_dir = os.getcwd()  # Get current working directory
print(f"Current directory: {current_dir}")

# List files in a directory
files = os.listdir(current_dir)
print(f"Files in current directory: {files}")

# Create a new directory
os.makedirs('fish_data', exist_ok=True)

# Rename a file
os.rename('fish_data.txt', 'fish_info.txt')

# Copy a file
shutil.copy('fish_info.txt', 'fish_data/fish_info_copy.txt')

# Move a file
shutil.move('fish_info.txt', 'fish_data/fish_info.txt')

# Delete a file
os.remove('fish_data/fish_info_copy.txt')

# Delete a directory
os.rmdir('empty_directory')  # Only works if directory is empty
shutil.rmtree('fish_data')  # Deletes directory and all contents (be careful!)
```

**Kurumi**: *[concerned]* Wow, that's a lot of power! I'll need to be careful with some of those operations, especially deleting files and directories.

**Jarvis**: *[nodding seriously]* Absolutely. Always double-check before using destructive operations like `os.remove()` or `shutil.rmtree()`. Now, let's talk about how to make all these file operations more robust with exception handling.

## Introduction to Exception Handling

**Kurumi**: *[returning to her original problem]* So, how do I prevent my program from crashing when a file doesn't exist?

**Jarvis**: This is where exception handling comes in. In Python, we use `try`/`except` blocks to catch and handle exceptions:

```python
try:
    # Code that might raise an exception
    with open('nonexistent_file.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    # Code to handle the exception
    print("The file does not exist. Creating it now...")
    with open('nonexistent_file.txt', 'w') as file:
        file.write("This is a new file.\n")
```

**Kurumi**: *[understanding dawning]* I see! So instead of letting the program crash, we "catch" the error and do something else instead.

**Jarvis**: Exactly! And Python has many built-in exception types for different kinds of errors. Here are some common ones:

- `FileNotFoundError`: When a file doesn't exist
- `PermissionError`: When you don't have permission to access a file
- `ZeroDivisionError`: When you try to divide by zero
- `ValueError`: When a function receives an argument of the correct type but inappropriate value
- `TypeError`: When an operation is performed on an object of inappropriate type
- `IndexError`: When you try to access an index that's out of range
- `KeyError`: When a dictionary key is not found

**Kurumi**: How do I handle different types of exceptions differently?

**Jarvis**: You can have multiple `except` blocks for different exception types:

```python
try:
    with open('fish_data.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print("The file does not exist")
except PermissionError:
    print("You don't have permission to read this file")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```

## The else and finally Clauses

**Kurumi**: Are there other parts to the `try`/`except` structure?

**Jarvis**: Yes, there are two additional clauses you can use: `else` and `finally`:

```python
try:
    with open('fish_data.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print("The file does not exist")
else:
    # This runs if no exception occurs
    print(f"File read successfully. Content length: {len(content)} characters")
finally:
    # This always runs, regardless of whether an exception occurred
    print("File operation attempted")
```

**Kurumi**: *[thinking]* So `else` is for code that should run only if no exception occurs, and `finally` is for cleanup code that should always run?

**Jarvis**: That's exactly right! The `finally` block is particularly useful for ensuring resources are properly released, although with context managers like `with open()`, this is less necessary for file operations.

## Raising Exceptions

**Kurumi**: Can I create my own exceptions?

**Jarvis**: Yes, you can both raise built-in exceptions and create your own custom exceptions. Let's start with raising exceptions:

```python
def check_fish_weight(weight):
    if weight <= 0:
        raise ValueError("Fish weight must be positive")
    return weight

try:
    fish_weight = check_fish_weight(-1.5)
except ValueError as e:
    print(f"Error: {e}")
```

**Kurumi**: And how do I create my own exception types?

**Jarvis**: You create custom exceptions by defining new classes that inherit from the built-in `Exception` class or one of its subclasses:

```python
class FishError(Exception):
    """Base class for fish-related exceptions"""
    pass

class InvalidFishWeightError(FishError):
    """Raised when the fish weight is invalid"""
    pass

class InvalidFishSpeciesError(FishError):
    """Raised when the fish species is invalid"""
    pass

def process_fish(species, weight):
    valid_species = ['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba']
    
    if species not in valid_species:
        raise InvalidFishSpeciesError(f"Unknown species: {species}")
    
    if weight <= 0:
        raise InvalidFishWeightError(f"Invalid weight: {weight}")
    
    return f"Processed {species} weighing {weight} kg"

try:
    result = process_fish('Shark', 100)
except InvalidFishSpeciesError as e:
    print(f"Species error: {e}")
except InvalidFishWeightError as e:
    print(f"Weight error: {e}")
except FishError as e:
    print(f"General fish error: {e}")
```

**Kurumi**: *[excited]* This is really powerful! I can see how this would make my programs much more robust.

## Exception Handling Best Practices

**Jarvis**: Let me share some best practices for exception handling:

1. **Be specific about which exceptions to catch**. Avoid catching all exceptions with a bare `except:` clause, as this can hide bugs.

2. **Don't catch exceptions you can't handle properly**. If you can't do anything meaningful with an exception, it's often better to let it propagate up.

3. **Use context managers** (`with` statement) when possible, as they automatically handle resource cleanup.

4. **Keep the try block as small as possible**, including only the code that might raise the exception you're trying to catch.

5. **Log exceptions** for debugging purposes, especially in production code.

**Kurumi**: These are great tips! Can you show me a real-world example that puts it all together?

**Jarvis**: Sure! Here's a robust function that converts a CSV file to JSON format, handling various exceptions that might occur:

```python
import csv
import json
import os

def convert_csv_to_json(csv_filename, json_filename):
    """
    Convert a CSV file to JSON format.
    
    Args:
        csv_filename: Path to the input CSV file
        json_filename: Path to the output JSON file
        
    Returns:
        bool: True if successful, False otherwise
    """
    try:
        # Check if input file exists
        if not os.path.exists(csv_filename):
            raise FileNotFoundError(f"Input file {csv_filename} does not exist")
        
        # Check if input file is readable
        if not os.access(csv_filename, os.R_OK):
            raise PermissionError(f"Cannot read from {csv_filename}")
        
        # Check if output directory is writable
        output_dir = os.path.dirname(json_filename) or '.'
        if not os.access(output_dir, os.W_OK):
            raise PermissionError(f"Cannot write to directory {output_dir}")
        
        # Read CSV data
        data = []
        with open(csv_filename, 'r', newline='') as csv_file:
            reader = csv.DictReader(csv_file)
            for row in reader:
                data.append(row)
        
        # Write JSON data
        with open(json_filename, 'w') as json_file:
            json.dump(data, json_file, indent=4)
        
        print(f"Successfully converted {csv_filename} to {json_filename}")
        return True
        
    except FileNotFoundError as e:
        print(f"Error: {e}")
        return False
    except PermissionError as e:
        print(f"Error: {e}")
        return False
    except csv.Error as e:
        print(f"CSV Error: {e}")
        return False
    except json.JSONDecodeError as e:
        print(f"JSON Error: {e}")
        return False
    except Exception as e:
        print(f"Unexpected error: {e}")
        return False
```

**Kurumi**: *[impressed]* This is really comprehensive! I can see how it checks for various potential issues before even attempting the conversion, and then handles different types of exceptions that might occur during the process.

**Jarvis**: Exactly! This function <response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>