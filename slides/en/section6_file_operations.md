# Section 6: File Operations and Exception Handling

## File Input/Output Operations

### Introduction to File I/O
- Files are used to store data persistently
- Python provides built-in functions and methods for file operations
- File operations typically follow a pattern: open, read/write, close

### Opening Files
```python
# Basic syntax for opening a file
file = open(filename, mode)

# Common file modes
# 'r' - Read (default)
# 'w' - Write (creates new file or truncates existing file)
# 'a' - Append (adds to end of file)
# 'b' - Binary mode
# 't' - Text mode (default)
# '+' - Read and write

# Examples
file = open('fish_data.txt', 'r')  # Open for reading
file = open('fish_data.txt', 'w')  # Open for writing
file = open('fish_data.txt', 'a')  # Open for appending
file = open('fish_data.bin', 'rb')  # Open binary file for reading
```

### Using Context Managers (with statement)
```python
# Recommended way to open files - automatically handles closing
with open('fish_data.txt', 'r') as file:
    # File operations here
    data = file.read()
    
# File is automatically closed when the block ends
```

### Reading from Files
```python
# Reading the entire file at once
with open('fish_data.txt', 'r') as file:
    content = file.read()
    print(content)

# Reading line by line
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

# Reading a specific line
with open('fish_data.txt', 'r') as file:
    lines = file.readlines()
    if len(lines) >= 3:
        third_line = lines[2]  # Get the third line (index 2)
        print(third_line)
```

### Writing to Files
```python
# Writing a string to a file
with open('fish_data.txt', 'w') as file:
    file.write("Koi: 1.2 kg, freshwater\n")
    file.write("Fugu: 2.5 kg, saltwater\n")
    file.write("Tai: 3.7 kg, saltwater\n")

# Writing multiple lines at once
lines = ["Koi: 1.2 kg, freshwater\n", 
         "Fugu: 2.5 kg, saltwater\n", 
         "Tai: 3.7 kg, saltwater\n"]
with open('fish_data.txt', 'w') as file:
    file.writelines(lines)

# Appending to a file
with open('fish_data.txt', 'a') as file:
    file.write("Unagi: 1.8 kg, freshwater\n")
    file.write("Saba: 2.9 kg, saltwater\n")
```

### File Positions and Seeking
```python
# Getting the current position
with open('fish_data.txt', 'r') as file:
    print(file.tell())  # 0 - start of file
    file.read(10)
    print(file.tell())  # 10 - after reading 10 characters

# Changing the position (seeking)
with open('fish_data.txt', 'r') as file:
    file.seek(10)  # Move to the 10th byte
    data = file.read(5)
    print(data)
    
    # seek(offset, whence)
    # whence: 0 = start (default), 1 = current position, 2 = end
    file.seek(0)  # Go back to the beginning
    file.seek(0, 2)  # Go to the end of the file
```

### Working with CSV Files
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

# Using DictReader and DictWriter
fish_dict_data = [
    {'Species': 'Koi', 'Weight (kg)': 1.2, 'Habitat': 'freshwater'},
    {'Species': 'Fugu', 'Weight (kg)': 2.5, 'Habitat': 'saltwater'},
    {'Species': 'Tai', 'Weight (kg)': 3.7, 'Habitat': 'saltwater'}
]

with open('fish_dict.csv', 'w', newline='') as file:
    fieldnames = ['Species', 'Weight (kg)', 'Habitat']
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(fish_dict_data)

with open('fish_dict.csv', 'r', newline='') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(f"{row['Species']}: {row['Weight (kg)']} kg, {row['Habitat']}")
```

### Working with JSON Files
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

# Converting Python objects to JSON strings
json_string = json.dumps(fish_data, indent=4)
print(json_string)

# Parsing JSON strings
parsed_data = json.loads(json_string)
print(parsed_data)
```

### File System Operations
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

## Exception Handling

### Introduction to Exceptions
- Exceptions are events that occur during program execution that disrupt the normal flow
- Python uses try/except blocks to handle exceptions
- Proper exception handling makes programs more robust and user-friendly

### Common Exceptions
```python
# Some common exceptions in Python:

# ZeroDivisionError
# result = 10 / 0

# TypeError
# result = "2" + 2

# ValueError
# number = int("abc")

# FileNotFoundError
# file = open("nonexistent_file.txt", "r")

# IndexError
# my_list = [1, 2, 3]
# item = my_list[10]

# KeyError
# my_dict = {"a": 1, "b": 2}
# value = my_dict["c"]

# AttributeError
# "hello".append("world")
```

### Basic Exception Handling
```python
# Basic try/except structure
try:
    # Code that might raise an exception
    file = open("fish_data.txt", "r")
    content = file.read()
    file.close()
except:
    # Code to handle the exception
    print("An error occurred while reading the file")

# Handling specific exceptions
try:
    file = open("fish_data.txt", "r")
    content = file.read()
    file.close()
except FileNotFoundError:
    print("The file does not exist")
except PermissionError:
    print("You don't have permission to read this file")
except:
    print("An unexpected error occurred")
```

### The else and finally Clauses
```python
# Using else clause - executed if no exception occurs
try:
    file = open("fish_data.txt", "r")
    content = file.read()
    file.close()
except FileNotFoundError:
    print("The file does not exist")
else:
    print(f"File read successfully. Content length: {len(content)} characters")

# Using finally clause - always executed
try:
    file = open("fish_data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("The file does not exist")
else:
    print(f"File read successfully. Content length: {len(content)} characters")
finally:
    print("File operation attempted")
    if 'file' in locals() and not file.closed:
        file.close()
        print("File closed")
```

### Raising Exceptions
```python
# Raising exceptions manually
def check_fish_weight(weight):
    if weight <= 0:
        raise ValueError("Fish weight must be positive")
    return weight

try:
    fish_weight = check_fish_weight(-1.5)
except ValueError as e:
    print(f"Error: {e}")

# Re-raising exceptions
try:
    fish_weight = check_fish_weight(-1.5)
except ValueError as e:
    print(f"Caught an error: {e}")
    raise  # Re-raise the same exception
```

### Creating Custom Exceptions
```python
# Defining custom exception classes
class FishError(Exception):
    """Base class for fish-related exceptions"""
    pass

class InvalidFishWeightError(FishError):
    """Raised when the fish weight is invalid"""
    pass

class InvalidFishSpeciesError(FishError):
    """Raised when the fish species is invalid"""
    pass

# Using custom exceptions
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

### Exception Handling Best Practices
```python
# 1. Be specific about which exceptions to catch
try:
    with open('fish_data.txt', 'r') as file:
        data = file.read()
except FileNotFoundError:
    print("File not found, creating a new one")
    with open('fish_data.txt', 'w') as file:
        file.write("New fish data file\n")

# 2. Don't catch exceptions you can't handle properly
try:
    # Complex operation
    pass
except Exception as e:
    # Log the error
    print(f"An error occurred: {e}")
    # Re-raise if you can't handle it
    raise

# 3. Use context managers (with statement) when possible
try:
    with open('fish_data.txt', 'r') as file:
        data = file.read()
    # No need to close the file - it's handled automatically
except FileNotFoundError:
    print("File not found")

# 4. Clean up resources in finally blocks
resource = None
try:
    resource = open('fish_data.txt', 'r')
    # Process the resource
except Exception as e:
    print(f"Error: {e}")
finally:
    if resource is not None:
        resource.close()
```

### Debugging with Exceptions
```python
# Using assertions for debugging
def calculate_fish_density(count, volume):
    assert volume > 0, "Volume must be positive"
    return count / volume

try:
    density = calculate_fish_density(10, 0)
except AssertionError as e:
    print(f"Assertion failed: {e}")

# Using exceptions for debugging
import traceback

try:
    # Some complex code
    result = 10 / 0
except Exception as e:
    print(f"Error: {e}")
    traceback.print_exc()  # Print the full traceback
```

### Exception Handling in File Operations
```python
# Robust file reading
def read_fish_data(filename):
    try:
        with open(filename, 'r') as file:
            return file.read()
    except FileNotFoundError:
        print(f"The file {filename} does not exist")
        return None
    except PermissionError:
        print(f"You don't have permission to read {filename}")
        return None
    except Exception as e:
        print(f"An unexpected error occurred: {e}")
        return None

# Robust file writing
def write_fish_data(filename, data):
    try:
        with open(filename, 'w') as file:
            file.write(data)
        return True
    except PermissionError:
        print(f"You don't have permission to write to {filename}")
        return False
    except Exception as e:
        print(f"An unexpected error occurred: {e}")
        return False

# Example usage
fish_data = """
Koi: 1.2 kg, freshwater
Fugu: 2.5 kg, saltwater
Tai: 3.7 kg, saltwater
"""

if write_fish_data('fish_data.txt', fish_data):
    print("Data written successfully")

content = read_fish_data('fish_data.txt')
if content:
    print("Read data:")
    print(content)
```

### Real-world Exception Handling Example
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

# Example usage
convert_csv_to_json('fish_data.csv', 'fish_data.json')
```
