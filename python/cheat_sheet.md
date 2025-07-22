# Python Cheat Sheet

A concise guide to Python for quick reference.

## 1. Basic Syntax & Variables

### Variable Declaration
Python is dynamically typed, so you don't need to declare variable types.

```python
# Numbers
integer_var = 10
float_var = 10.5

# Strings
string_var = "Hello, World!"

# Booleans
boolean_var = True

# None Type
none_var = None
```

## 2. Data Structures

### Lists (Dynamic Arrays)
Mutable, ordered sequence of elements.

```python
# Declaration
my_list = [1, 2, "three", 4.0]
empty_list = []

# Accessing elements
first_element = my_list[0]  # 1
last_element = my_list[-1] # 4.0

# Slicing
sub_list = my_list[1:3]  # [2, "three"]

# Adding elements
my_list.append(5)        # [1, 2, "three", 4.0, 5]
my_list.insert(1, "new") # [1, "new", 2, "three", 4.0, 5]

# Removing elements
my_list.pop()      # Removes and returns the last element
my_list.remove("new") # Removes the first occurrence of "new"

# List Comprehensions
squares = [x**2 for x in range(5)] # [0, 1, 4, 9, 16]
```

### Hashmaps (Dictionaries)
Mutable, unordered key-value pairs.

```python
# Declaration
my_dict = {"name": "Alice", "age": 30}
empty_dict = {}

# Accessing values
name = my_dict["name"] # "Alice"
age = my_dict.get("age") # 30 (safer, returns None if key doesn't exist)

# Adding/Updating
my_dict["city"] = "New York"
my_dict["age"] = 31

# Removing items
del my_dict["city"]
age = my_dict.pop("age") # Removes "age" and returns its value

# Iterating
for key, value in my_dict.items():
    print(f"{key}: {value}")

# Dictionary Comprehensions
squares_dict = {x: x**2 for x in range(5)} # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### Graph Node Representation
A simple graph can be represented using a dictionary (adjacency list).

```python
# Adjacency List
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

# Node class (for more complex graphs)
class GraphNode:
    def __init__(self, value):
        self.value = value
        self.neighbors = []

node_a = GraphNode('A')
node_b = GraphNode('B')
node_a.neighbors.append(node_b)
```

## 3. Control Flow

### For Loop Variations

```python
items = ["a", "b", "c"]

# Basic for loop
for item in items:
    print(item)

# Loop with index (enumerate)
for i, item in enumerate(items):
    print(f"Index {i}: {item}")

# Loop over two lists (zip)
list1 = [1, 2, 3]
list2 = ["one", "two", "three"]
for num, name in zip(list1, list2):
    print(f"{num} is {name}")
```

### Iterators
An iterator is an object that contains a countable number of values.

```python
my_list = [1, 2, 3]
my_iterator = iter(my_list)

print(next(my_iterator)) # 1
print(next(my_iterator)) # 2

# Custom iterator
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self
  def __next__(self):
    if self.a <= 5:
      x = self.a
      self.a += 1
      return x
    else:
      raise StopIteration

my_class = MyNumbers()
my_iter = iter(my_class)
for x in my_iter:
  print(x)
```

## 4. Functions

### Lambda Functions
Small anonymous functions.

```python
# lambda arguments: expression
add = lambda a, b: a + b
print(add(5, 3)) # 8

# Used in functions like map, filter
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
evens = list(filter(lambda x: x % 2 == 0, numbers))
```

### Recursion
A function that calls itself.

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5)) # 120
```

## 5. Object-Oriented Programming (OOP)

### Class Declarations
`self` refers to the instance of the class.

```python
class Dog:
    # Class attribute
    species = "Canis familiaris"

    # Initializer / Instance attributes
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # Instance method
    def description(self):
        return f"{self.name} is {self.age} years old."

    # Another instance method
    def speak(self, sound):
        return f"{self.name} says {sound}."

# Creating an instance
my_dog = Dog("Buddy", 3)

# Calling methods
print(my_dog.description())
print(my_dog.speak("Woof"))
```

## 6. String Operations

### Splitting and Joining

```python
my_string = "hello world python"

# Split string into a list
words = my_string.split(' ') # ['hello', 'world', 'python']

# Join a list of strings into a single string
joined_string = "-".join(words) # "hello-world-python"
```

### Common String Methods
```python
s = "  Hello, World!  "
s.strip()         # "Hello, World!" (removes leading/trailing whitespace)
s.lower()         # "  hello, world!  "
s.upper()         # "  HELLO, WORLD!  "
s.replace("World", "Python") # "  Hello, Python!  "
s.startswith("  H") # True
s.endswith("!  ")   # True
```

## 7. Pointers in Python (References)

Python does not have pointers in the C/C++ sense. Instead, variables are references to objects in memory.

```python
# Immutable types (int, str, tuple): Reassignment creates a new object.
x = 10
y = x
y = 20 # x remains 10, y now refers to a new object with value 20.
print(x) # 10

# Mutable types (list, dict): Changes to the object are reflected in all references.
list_a = [1, 2, 3]
list_b = list_a
list_b.append(4) # This modifies the original list object.
print(list_a) # [1, 2, 3, 4]
```

## 8. Copying Objects

To avoid unintended modifications of mutable objects, you can create copies.

### Shallow Copy
Creates a new object but inserts references to the items found in the original.

```python
import copy

list_a = [[1, 2], [3, 4]]
list_b = copy.copy(list_a) # Shallow copy

list_b.append([5, 6])
print(f"List A: {list_a}") # [[1, 2], [3, 4]]
print(f"List B: {list_b}") # [[1, 2], [3, 4], [5, 6]]

# Modifying a nested object in the copy affects the original
list_b[0][0] = 99
print(f"List A after change: {list_a}") # [[99, 2], [3, 4]]
print(f"List B after change: {list_b}") # [[99, 2], [3, 4], [5, 6]]
```

### Deep Copy
Creates a new object and recursively copies all objects found in the original.

```python
import copy

list_a = [[1, 2], [3, 4]]
list_c = copy.deepcopy(list_a) # Deep copy

# Modifying a nested object in the deep copy does NOT affect the original
list_c[0][0] = 99
print(f"List A: {list_a}") # [[1, 2], [3, 4]]
print(f"List C: {list_c}") # [[99, 2], [3, 4]]
```

## 9. Threading and Locking

The `threading` module allows you to run multiple threads (lightweight processes) concurrently.

### Basic Threading
```python
import threading
import time

def my_function(name):
    print(f"Thread {name}: starting")
    time.sleep(2)
    print(f"Thread {name}: finishing")

# Create and start threads
thread1 = threading.Thread(target=my_function, args=("One",))
thread2 = threading.Thread(target=my_function, args=("Two",))
thread1.start()
thread2.start()

# Wait for both threads to complete
thread1.join()
thread2.join()

print("All threads finished.")
```

### Using Locks
A lock is used to protect shared resources from being accessed by multiple threads at the same time.

```python
import threading
import time

shared_resource = 0
lock = threading.Lock()

def worker():
    global shared_resource
    lock.acquire()
    try:
        # Critical section that needs protection
        local_copy = shared_resource
        local_copy += 1
        time.sleep(0.1) # Simulate work
        shared_resource = local_copy
    finally:
        lock.release() # Always release the lock

threads = []
for i in range(5):
    t = threading.Thread(target=worker)
    threads.append(t)
    t.start()

for t in threads:
    t.join()

print(f"Final value of shared resource: {shared_resource}") # Should be 5
```
