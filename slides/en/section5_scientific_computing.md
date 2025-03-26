# Section 5: Scientific Computing

## Basics of the NumPy Library

### Introduction to NumPy
- NumPy (Numerical Python) is a fundamental package for scientific computing in Python
- Provides support for large, multi-dimensional arrays and matrices
- Includes a large collection of high-level mathematical functions
- Core library for many scientific and data analysis packages

### Installing NumPy
```python
# Install NumPy using pip
pip install numpy

# Import NumPy in your Python code
import numpy as np  # Standard convention is to import as 'np'
```

### NumPy Arrays
- The fundamental object in NumPy is the `ndarray` (n-dimensional array)
- Advantages over Python lists:
  - More compact storage
  - Faster access for reading and writing elements
  - Vectorized operations for efficient computation
  - Broadcasting capabilities

```python
# Creating NumPy arrays
import numpy as np

# From a Python list
fish_weights = np.array([1.2, 2.5, 3.7, 1.8, 2.9])
print(fish_weights)  # [1.2 2.5 3.7 1.8 2.9]

# Using NumPy functions
zeros = np.zeros(5)  # Array of 5 zeros
print(zeros)  # [0. 0. 0. 0. 0.]

ones = np.ones(5)  # Array of 5 ones
print(ones)  # [1. 1. 1. 1. 1.]

# Range of values
range_array = np.arange(0, 10, 2)  # Start, stop, step
print(range_array)  # [0 2 4 6 8]

# Evenly spaced values
linspace = np.linspace(0, 1, 5)  # Start, stop, number of points
print(linspace)  # [0.   0.25 0.5  0.75 1.  ]

# Random values
random_array = np.random.rand(5)  # 5 random values between 0 and 1
print(random_array)
```

### Array Attributes and Methods
```python
# Array attributes
fish_weights = np.array([1.2, 2.5, 3.7, 1.8, 2.9])

print(fish_weights.shape)  # (5,) - dimensions of the array
print(fish_weights.size)   # 5 - number of elements
print(fish_weights.dtype)  # float64 - data type
print(fish_weights.ndim)   # 1 - number of dimensions

# Array methods
print(fish_weights.sum())    # 12.1 - sum of all elements
print(fish_weights.mean())   # 2.42 - mean value
print(fish_weights.std())    # 0.8738... - standard deviation
print(fish_weights.min())    # 1.2 - minimum value
print(fish_weights.max())    # 3.7 - maximum value
print(fish_weights.argmin()) # 0 - index of minimum value
print(fish_weights.argmax()) # 2 - index of maximum value
```

### Multi-dimensional Arrays
```python
# Creating 2D arrays
fish_data = np.array([
    [1.2, 2.5, 3.7],  # Koi weights
    [0.8, 1.5, 2.2],  # Goldfish weights
    [3.2, 4.5, 5.1]   # Fugu weights
])

print(fish_data.shape)  # (3, 3) - 3 rows, 3 columns
print(fish_data.ndim)   # 2 - 2 dimensions

# Accessing elements
print(fish_data[0, 0])  # 1.2 - first row, first column
print(fish_data[2, 1])  # 4.5 - third row, second column

# Accessing rows and columns
print(fish_data[0])     # [1.2 2.5 3.7] - first row
print(fish_data[:, 1])  # [2.5 1.5 4.5] - second column

# Creating 3D arrays
tank_data = np.array([
    [  # Tank 1
        [1.2, 2.5, 3.7],  # Koi weights
        [0.8, 1.5, 2.2],  # Goldfish weights
    ],
    [  # Tank 2
        [3.2, 4.5, 5.1],  # Fugu weights
        [2.1, 3.3, 4.2]   # Tai weights
    ]
])

print(tank_data.shape)  # (2, 2, 3) - 2 tanks, 2 fish types per tank, 3 fish per type
print(tank_data.ndim)   # 3 - 3 dimensions
```

### Array Indexing and Slicing
```python
# 1D array indexing and slicing
fish_weights = np.array([1.2, 2.5, 3.7, 1.8, 2.9])

print(fish_weights[0])     # 1.2 - first element
print(fish_weights[-1])    # 2.9 - last element
print(fish_weights[1:4])   # [2.5 3.7 1.8] - elements from index 1 to 3
print(fish_weights[:3])    # [1.2 2.5 3.7] - elements from start to index 2
print(fish_weights[2:])    # [3.7 1.8 2.9] - elements from index 2 to end
print(fish_weights[::2])   # [1.2 3.7 2.9] - every second element

# 2D array indexing and slicing
fish_data = np.array([
    [1.2, 2.5, 3.7],  # Koi weights
    [0.8, 1.5, 2.2],  # Goldfish weights
    [3.2, 4.5, 5.1]   # Fugu weights
])

print(fish_data[0, 0])     # 1.2 - first row, first column
print(fish_data[0])        # [1.2 2.5 3.7] - first row
print(fish_data[:, 0])     # [1.2 0.8 3.2] - first column
print(fish_data[0:2, 1:3]) # [[2.5 3.7], [1.5 2.2]] - first two rows, second and third columns
```

### Boolean Indexing
```python
fish_weights = np.array([1.2, 2.5, 3.7, 1.8, 2.9])

# Create a boolean mask
large_fish = fish_weights > 2.0
print(large_fish)  # [False  True  True False  True]

# Use the mask to filter the array
print(fish_weights[large_fish])  # [2.5 3.7 2.9]

# Combine conditions
medium_fish = (fish_weights > 1.5) & (fish_weights < 3.0)
print(medium_fish)  # [False  True False  True  True]
print(fish_weights[medium_fish])  # [2.5 1.8 2.9]

# Count elements that satisfy a condition
print(np.sum(fish_weights > 2.0))  # 3 - number of fish weighing more than 2.0
```

### Array Operations
```python
# Arithmetic operations
fish_weights = np.array([1.2, 2.5, 3.7, 1.8, 2.9])

print(fish_weights + 1)     # [2.2 3.5 4.7 2.8 3.9] - add 1 to each element
print(fish_weights * 2)     # [2.4 5.0 7.4 3.6 5.8] - multiply each element by 2
print(fish_weights ** 2)    # [1.44 6.25 13.69 3.24 8.41] - square each element
print(np.sqrt(fish_weights)) # [1.095... 1.581... 1.923... 1.341... 1.702...] - square root of each element

# Operations between arrays
fish_weights1 = np.array([1.2, 2.5, 3.7])
fish_weights2 = np.array([0.8, 1.5, 2.2])

print(fish_weights1 + fish_weights2)  # [2.0 4.0 5.9] - element-wise addition
print(fish_weights1 * fish_weights2)  # [0.96 3.75 8.14] - element-wise multiplication

# Aggregation operations
fish_data = np.array([
    [1.2, 2.5, 3.7],  # Koi weights
    [0.8, 1.5, 2.2],  # Goldfish weights
    [3.2, 4.5, 5.1]   # Fugu weights
])

print(np.sum(fish_data))         # 24.7 - sum of all elements
print(np.sum(fish_data, axis=0)) # [5.2 8.5 11.0] - sum of each column
print(np.sum(fish_data, axis=1)) # [7.4 4.5 12.8] - sum of each row

print(np.mean(fish_data))         # 2.7444... - mean of all elements
print(np.mean(fish_data, axis=0)) # [1.7333... 2.8333... 3.6666...] - mean of each column
print(np.mean(fish_data, axis=1)) # [2.4666... 1.5 4.2666...] - mean of each row
```

### Broadcasting
- Broadcasting allows NumPy to perform operations on arrays of different shapes
- Rules for broadcasting:
  1. If arrays don't have the same rank, prepend the shape of the lower-rank array with 1s
  2. If the shape of the arrays doesn't match in any dimension, expand the array with shape 1 in that dimension
  3. If the shape of the arrays doesn't match in any dimension and neither is 1, raise an error

```python
# Broadcasting examples
fish_weights = np.array([1.2, 2.5, 3.7])  # Shape: (3,)
growth_factors = np.array([1.1, 1.2, 1.3])  # Shape: (3,)

# Same shape: element-wise multiplication
print(fish_weights * growth_factors)  # [1.32 3.0 4.81]

# Broadcasting with a scalar
print(fish_weights * 2)  # [2.4 5.0 7.4]

# Broadcasting with arrays of different shapes
fish_data = np.array([
    [1.2, 2.5, 3.7],  # Koi weights
    [0.8, 1.5, 2.2],  # Goldfish weights
    [3.2, 4.5, 5.1]   # Fugu weights
])  # Shape: (3, 3)

growth_factor = np.array([1.1, 1.2, 1.3])  # Shape: (3,)

# Broadcasting: (3, 3) * (3,) -> (3, 3) * (1, 3) -> (3, 3)
# Each row is multiplied by the corresponding growth factor
print(fish_data * growth_factor)
# [[1.32 3.0  4.81]
#  [0.88 1.8  2.86]
#  [3.52 5.4  6.63]]
```

### Reshaping Arrays
```python
# Reshaping arrays
fish_weights = np.array([1.2, 2.5, 3.7, 1.8, 2.9, 3.1])

# Reshape to 2x3 array
reshaped = fish_weights.reshape(2, 3)
print(reshaped)
# [[1.2 2.5 3.7]
#  [1.8 2.9 3.1]]

# Reshape to 3x2 array
reshaped = fish_weights.reshape(3, 2)
print(reshaped)
# [[1.2 2.5]
#  [3.7 1.8]
#  [2.9 3.1]]

# Using -1 to automatically determine the size of one dimension
reshaped = fish_weights.reshape(-1, 2)  # -1 means "figure out this dimension"
print(reshaped)
# [[1.2 2.5]
#  [3.7 1.8]
#  [2.9 3.1]]

# Flattening an array
fish_data = np.array([
    [1.2, 2.5, 3.7],
    [0.8, 1.5, 2.2]
])
flattened = fish_data.flatten()
print(flattened)  # [1.2 2.5 3.7 0.8 1.5 2.2]

# Transposing an array (swapping rows and columns)
transposed = fish_data.T
print(transposed)
# [[1.2 0.8]
#  [2.5 1.5]
#  [3.7 2.2]]
```

### Random Number Generation
```python
# Random number generation
import numpy as np

# Random floats between 0 and 1
random_floats = np.random.rand(5)
print(random_floats)

# Random integers between 0 and 10
random_ints = np.random.randint(0, 10, 5)
print(random_ints)

# Random values from a normal distribution
random_normal = np.random.normal(loc=0, scale=1, size=5)  # mean=0, std=1
print(random_normal)

# Setting a random seed for reproducibility
np.random.seed(42)
print(np.random.rand(3))  # Always the same 3 random numbers

# Shuffling an array
fish_types = np.array(['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba'])
np.random.shuffle(fish_types)
print(fish_types)
```

### Linear Algebra Operations
```python
# Linear algebra operations
import numpy as np

# Matrix multiplication
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(np.dot(A, B))  # Matrix multiplication using dot()
# [[19 22]
#  [43 50]]

print(A @ B)  # Matrix multiplication using @ operator (Python 3.5+)
# [[19 22]
#  [43 50]]

# Determinant
print(np.linalg.det(A))  # -2.0

# Inverse
print(np.linalg.inv(A))
# [[-2.   1. ]
#  [ 1.5 -0.5]]

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)
print("Eigenvalues:", eigenvalues)
print("Eigenvectors:", eigenvectors)

# Solving linear equations: Ax = b
A = np.array([[1, 2], [3, 4]])
b = np.array([5, 6])
x = np.linalg.solve(A, b)
print("Solution to Ax = b:", x)
```

### Saving and Loading NumPy Arrays
```python
# Saving and loading arrays
import numpy as np

# Create an array
fish_data = np.array([
    [1.2, 2.5, 3.7],
    [0.8, 1.5, 2.2],
    [3.2, 4.5, 5.1]
])

# Save to a binary file
np.save('fish_data.npy', fish_data)

# Load from a binary file
loaded_data = np.load('fish_data.npy')
print(loaded_data)

# Save to a text file
np.savetxt('fish_data.csv', fish_data, delimiter=',')

# Load from a text file
loaded_data = np.loadtxt('fish_data.csv', delimiter=',')
print(loaded_data)
```

## Basics of the Pandas Library

### Introduction to Pandas
- Pandas is a powerful data manipulation and analysis library
- Built on top of NumPy
- Provides data structures for efficiently storing and manipulating tabular data
- Includes tools for reading and writing data, handling missing values, filtering, grouping, and more
- Essential for data science and data analysis in Python

### Installing Pandas
```python
# Install Pandas using pip
pip install pandas

# Import Pandas in your Python code
import pandas as pd  # Standard convention is to import as 'pd'
```

### Pandas Data Structures
- Series: 1D labeled array (like a column in a table)
- DataFrame: 2D labeled data structure (like a table with rows and columns)

```python
# Creating a Series
import pandas as pd
import numpy as np

# From a list
fish_weights = pd.Series([1.2, 2.5, 3.7, 1.8, 2.9])
print(fish_weights)
# 0    1.2
# 1    2.5
# 2    3.7
# 3    1.8
# 4    2.9
# dtype: float64

# With custom index
fish_weights = pd.Series([1.2, 2.5, 3.7, 1.8, 2.9], index=['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba'])
print(fish_weights)
# Koi      1.2
# Fugu     2.5
# Tai      3.7
# Unagi    1.8
# Saba     2.9
# dtype: float64

# From a dictionary
fish_dict = {'Koi': 1.2, 'Fugu': 2.5, 'Tai': 3.7, 'Unagi': 1.8, 'Saba': 2.9}
fish_weights = pd.Series(fish_dict)
print(fish_weights)
# Koi      1.2
# Fugu     2.5
# Tai      3.7
# Unagi    1.8
# Saba     2.9
# dtype: float64

# Creating a DataFrame
# From a dictionary of lists
fish_data = {
    'weight': [1.2, 2.5, 3.7, 1.8, 2.9],
    'length': [25, 30, 40, 28, 35],
    'habitat': ['freshwater', 'saltwater', 'saltwater', 'freshwater', 'saltwater']
}
fish_df = pd.DataFrame(fish_data, index=['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba'])
print(fish_df)
#       weight  length    habitat
# Koi      1.2      25  freshwater
# Fugu     2.5      30   saltwater
# Tai      3.7      40   saltwater
# Unagi    1.8      28  freshwater
# Saba     2.9      35   saltwater

# From a list of dictionaries
fish_list = [
    {'name': 'Koi', 'weight': 1.2, 'habitat': 'freshwater'},
    {'name': 'Fugu', 'weight': 2.5, 'habitat': 'saltwater'},
    {'name': 'Tai', 'weight': 3.7, 'habitat': 'saltwater'}
]
fish_df = pd.DataFrame(fish_list)
print(fish_df)
#    name  weight    habitat
# 0   Koi     1.2  freshwater
# 1  Fugu     2.5   saltwater
# 2   Tai     3.7   saltwater

# From a NumPy array
data = np.array([[1.2, 25, 1], [2.5, 30, 0], [3.7, 40, 0]])
fish_df = pd.DataFrame(data, index=['Koi', 'Fugu', 'Tai'], 
                      columns=['weight', 'length', 'is_freshwater'])
print(fish_df)
#       weight  length  is_freshwater
# Koi      1.2    25.0           1.0
# Fugu     2.5    30.0           0.0
# Tai      3.7    40.0           0.0
```

### Accessing Data in DataFrames
```python
# Create a sample DataFrame
fish_data = {
    'weight': [1.2, 2.5, 3.7, 1.8, 2.9],
    'length': [25, 30, 40, 28, 35],
    'habitat': ['freshwater', 'saltwater', 'saltwater', 'freshwater', 'saltwater']
}
fish_df = pd.DataFrame(fish_data, index=['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba'])

# Accessing columns
print(fish_df['weight'])  # Access a single column
print(fish_df[['weight', 'length']])  # Access multiple columns

# Accessing rows using .loc (label-based)
print(fish_df.loc['Koi'])  # Access a single row
print(fish_df.loc[['Koi', 'Fugu']])  # Access multiple rows
print(fish_df.loc['Koi', 'weight'])  # Access a specific value
print(fish_df.loc[['Koi', 'Fugu'], ['weight', 'habitat']])  # Access a subset

# Accessing rows using .iloc (integer-based)
print(fish_df.iloc[0])  # Access the first row
print(fish_df.iloc[[0, 1]])  # Access the first two rows
print(fish_df.iloc[0, 0])  # Access the first value
print(fish_df.iloc[0:2, 0:2])  # Access a subset using slices

# Boolean indexing
print(fish_df[fish_df['weight'] > 2.0])  # Rows where weight > 2.0
print(fish_df[fish_df['habitat'] == 'freshwater'])  # Rows with freshwater habitat
```

### Basic DataFrame Operations
```python
# Create a sample DataFrame
fish_data = {
    'weight': [1.2, 2.5, 3.7, 1.8, 2.9],
    'length': [25, 30, 40, 28, 35],
    'habitat': ['freshwater', 'saltwater', 'saltwater', 'freshwater', 'saltwater']
}
fish_df = pd.DataFrame(fish_data, index=['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba'])

# Basic information
print(fish_df.shape)  # (5, 3) - 5 rows, 3 columns
print(fish_df.dtypes)  # Data types of each column
print(fish_df.info())  # Summary of the DataFrame
print(fish_df.describe())  # Statistical summary of numeric columns

# Adding a new column
fish_df['price'] = [1000, 5000, 3000, 2000, 1500]
print(fish_df)

# Adding a calculated column
fish_df['price_per_kg'] = fish_df['price'] / fish_df['weight']
print(fish_df)

# Deleting columns
fish_df_copy = fish_df.copy()
fish_df_copy = fish_df_copy.drop('price_per_kg', axis=1)  # axis=1 for columns
print(fish_df_copy)

# Renaming columns
fish_df_renamed = fish_df.rename(columns={'weight': 'weight_kg', 'length': 'length_cm'})
print(fish_df_renamed)

# Sorting
print(fish_df.sort_values('weight'))  # Sort by weight (ascending)
print(fish_df.sort_values('weight', ascending=False))  # Sort by weight (descending)
print(fish_df.sort_values(['habitat', 'weight']))  # Sort by habitat, then weight
```

### Handling Missing Data
```python
# Create a DataFrame with missing values
import numpy as np
import pandas as pd

fish_data = {
    'weight': [1.2, 2.5, np.nan, 1.8, 2.9],
    'length': [25, np.nan, 40, 28, 35],
    'habitat': ['freshwater', 'saltwater', None, 'freshwater', 'saltwater']
}
fish_df = pd.DataFrame(fish_data, index=['Koi', 'Fugu', 'Tai', 'Unagi', 'Saba'])
print(fish_df)

# Checking for missing values
print(fish_df.isnull())  # Boolean mask of missing values
print(fish_df.isnull().sum())  # Count of missing values per column

# Dropping missing values
print(fish_df.dropna())  # Drop rows with<response clipped><NOTE>To save on context only part of this file has been shown to you. You should retry this tool after you have searched inside the file with `grep -n` in order to find the line numbers of what you are looking for.</NOTE>