# Section 6: File Operations and Exception Handling - Homework Assignments

## File Input/Output Operations

### Exercise 1: Basic File Operations
1. Create a text file named `fish_inventory.txt` with the following content:
   ```
   Koi,1.2,freshwater
   Fugu,2.5,saltwater
   Tai,3.7,saltwater
   Unagi,1.8,freshwater
   Saba,2.9,saltwater
   ```

2. Write a Python program that reads this file and prints each line with line numbers.

3. Modify your program to parse each line and print the data in a more readable format:
   ```
   Fish #1: Koi (1.2 kg) - Habitat: freshwater
   Fish #2: Fugu (2.5 kg) - Habitat: saltwater
   ...
   ```

4. Create a new file called `freshwater_fish.txt` that contains only the freshwater fish from the original file.

5. Create a new file called `saltwater_fish.txt` that contains only the saltwater fish from the original file.

### Exercise 2: File Analysis
1. Write a program that reads the `fish_inventory.txt` file and calculates:
   - The total number of fish
   - The average weight of all fish
   - The number of freshwater and saltwater fish
   - The heaviest fish and its species
   - The lightest fish and its species

2. Write the analysis results to a new file called `fish_analysis.txt` in a readable format.

3. Modify your program to handle the case where the file doesn't exist or has an invalid format.

### Exercise 3: CSV and JSON Operations
1. Convert the `fish_inventory.txt` file to a CSV file named `fish_inventory.csv` with proper headers.

2. Read the CSV file and convert it to a JSON file named `fish_inventory.json`.

3. Add two more fish to the JSON file:
   - Hamachi: 4.5 kg, saltwater
   - Ayu: 0.3 kg, freshwater

4. Read the updated JSON file and convert it back to a CSV file named `updated_fish_inventory.csv`.

5. Create a function that can convert between CSV and JSON formats based on a parameter.

### Exercise 4: File System Operations
1. Create a directory structure for organizing fish data:
   ```
   fish_data/
   ├── freshwater/
   ├── saltwater/
   └── metadata/
   ```

2. Write a program that reads the `fish_inventory.txt` file and creates individual files for each fish in the appropriate directory (freshwater or saltwater).

3. Create a metadata file in the metadata directory that lists all the files created and their locations.

4. Write a function that can search for a fish by name and return its file path.

5. Create a backup function that copies all fish files to a `backup` directory with a timestamp in the filename.

## Exception Handling

### Exercise 1: Basic Exception Handling
1. Write a function called `safe_divide(a, b)` that performs division but handles the case where `b` is zero by returning None.

2. Write a function called `safe_convert_to_int(s)` that converts a string to an integer but handles the case where the string is not a valid integer.

3. Write a function called `safe_open_file(filename)` that opens a file but handles the case where the file doesn't exist by creating it.

4. Write a function called `safe_get_element(lst, index)` that gets an element from a list but handles the case where the index is out of range.

5. Write a function called `safe_get_key(d, key)` that gets a value from a dictionary but handles the case where the key doesn't exist.

### Exercise 2: Custom Exceptions
1. Create a custom exception hierarchy for a fish inventory system:
   - `FishError` (base class)
   - `InvalidFishSpeciesError`
   - `InvalidFishWeightError`
   - `InvalidFishHabitatError`

2. Write a function called `validate_fish(species, weight, habitat)` that validates fish data and raises the appropriate exception if the data is invalid.

3. Write a function called `add_fish_to_inventory(inventory, species, weight, habitat)` that adds a fish to an inventory but handles any validation errors.

4. Create a test program that demonstrates the use of your custom exceptions.

5. Modify your program to log all exceptions to a file called `error_log.txt`.

### Exercise 3: File Processing with Exception Handling
1. Write a robust function called `process_fish_file(input_file, output_file)` that:
   - Reads fish data from the input file
   - Validates each fish (using your validation function from Exercise 2)
   - Writes valid fish to the output file
   - Keeps track of any errors encountered

2. The function should handle the following exceptions:
   - File not found
   - Permission errors
   - Invalid data format
   - Custom fish validation errors

3. The function should return a tuple containing:
   - The number of fish successfully processed
   - The number of errors encountered
   - A list of error messages

4. Create a test program that demonstrates the use of your function with various input files (valid, invalid, nonexistent).

5. Modify your function to create a detailed report of the processing results.

### Exercise 4: Robust Data Conversion
1. Write a robust function called `convert_file_format(input_file, output_file, format_from, format_to)` that converts between different file formats:
   - Text (one record per line)
   - CSV
   - JSON

2. The function should handle all possible exceptions and provide meaningful error messages.

3. The function should validate the data during conversion and skip invalid records.

4. The function should create a backup of the input file before processing.

5. Create a test program that demonstrates the use of your function with various input files and formats.

## Combined Exercises

### Exercise 1: Fish Database System
Create a simple fish database system that:

1. Stores fish data in a JSON file.
2. Provides functions to:
   - Add a fish
   - Remove a fish
   - Update a fish
   - Search for fish by various criteria (species, weight range, habitat)
   - Generate reports (total fish, average weight, etc.)

3. Implements proper exception handling for all operations.

4. Provides a simple command-line interface for interacting with the database.

5. Logs all operations and errors to a file.

### Exercise 2: Fish Data Analysis Tool
Create a tool that:

1. Reads fish data from various file formats (text, CSV, JSON).
2. Performs statistical analysis on the data:
   - Average weight by species
   - Average weight by habitat
   - Weight distribution
   - Habitat distribution

3. Generates reports in various formats (text, CSV, JSON).

4. Implements proper exception handling for all operations.

5. Provides a simple command-line interface for specifying input files, analysis options, and output formats.

### Exercise 3: Fish Inventory Management System
Create a more advanced version of the fish database system that:

1. Uses a directory structure to organize fish data by habitat.
2. Stores individual fish data in separate files.
3. Maintains an index file for quick searching.
4. Implements file locking to prevent concurrent modifications.
5. Provides backup and restore functionality.
6. Implements proper exception handling for all operations.
7. Logs all operations and errors to a file.

### Exercise 4: Data Migration Tool
Create a tool that:

1. Reads fish data from an old format (e.g., fixed-width text file).
2. Validates and cleans the data.
3. Converts the data to a new format (e.g., JSON).
4. Handles errors gracefully and provides detailed error reports.
5. Allows for partial migrations (e.g., only freshwater fish).
6. Provides a simple command-line interface for specifying migration options.

## Submission Guidelines
1. Submit your solutions as Python scripts or Jupyter notebooks.
2. Include comments explaining your approach and any assumptions made.
3. Make sure your code is well-organized and follows PEP 8 style guidelines.
4. Test your code with various inputs to ensure it works correctly.
5. Include a brief report describing your solution and any challenges you encountered.

## Bonus Challenge
Create a comprehensive fish inventory management system that combines all the concepts covered in this section:
- File I/O operations
- Exception handling
- Custom exceptions
- File format conversion
- Data validation
- Logging
- Backup and restore

The system should be robust, user-friendly, and well-documented.

Good luck!
