#Dictionary
https://www.geeksforgeeks.org/python/python-dictionary/


**Python dictionary** is a data structure that stores the value in **key: value** pairs. Values in a dictionary can be of any data type and can be duplicated, whereas keys can't be repeated and must be **immutable**.

**Example:** Here, The data is stored in **key:value** pairs in dictionaries, which makes it easier to find values.
```python
d = {1: 'Geeks', 2: 'For', 3: 'Geeks'}
print(d)
# {1: 'Geeks', 2: 'For', 3: 'Geeks'}
```


## How to Create a Dictionary
Dictionary can be created by placing a sequence of elements within curly {} braces, separated by a 'comma'.
```python
d1 = {1: 'Geeks', 2: 'For', 3: 'Geeks'}
print(d1)

# create dictionary using dict() constructor
d2 = dict(a = "Geeks", b = "for", c = "Geeks")
print(d2)
# {1: 'Geeks', 2: 'For', 3: 'Geeks'}
# {'a': 'Geeks', 'b': 'for', 'c': 'Geeks'}
```
- **Dictionary keys are case sensitive:** the same name but different cases of Key will be treated distinctly.
- **Keys must be immutable:** This means keys can be strings, numbers or tuples but not lists.
- **Keys must be unique:** Duplicate keys are not allowed and any duplicate key will overwrite the previous value.
- Dictionary internally uses [Hashing](https://www.geeksforgeeks.org/dsa/introduction-to-hashing-2/). Hence, operations like search, insert, delete can be performed in **Constant Time**.


## Accessing Dictionary Items
We can access a value from a dictionary by using the **key** within square brackets or [**g**et()](https://www.geeksforgeeks.org/python/python-dictionary-get-method/) method.
```python
d = { "name": "Prajjwal", 1: "Python", (1, 2): [1,2,4] }

# Access using key
print(d["name"])

# Access using get()
print(d.get("name"))
# Prajjwal
# Prajjwal
```


## Adding and Updating Dictionary Items
We can add new key-value pairs or update existing keys by using assignment.
```python
d = {1: 'Geeks', 2: 'For', 3: 'Geeks'}

# Adding a new key-value pair
d["age"] = 22

# Updating an existing value
d[1] = "Python dict"

print(d)
# {1: 'Python dict', 2: 'For', 3: 'Geeks', 'age': 22}
```


## Removing Dictionary Items
We can remove items from dictionary using the following methods:

- [**del**](https://www.geeksforgeeks.org/python/python-del-to-delete-objects/): Removes an item by key.
- [**pop()**](https://www.geeksforgeeks.org/python/python-dictionary-pop-method/): Removes an item by key and returns its value.
- [**clear()**](https://www.geeksforgeeks.org/python/python-dictionary-clear/): Empties the dictionary.
- [**popitem()**](https://www.geeksforgeeks.org/python/python-dictionary-popitem-method/): Removes and returns the last key-value pair.
```python
d = {1: 'Geeks', 2: 'For', 3: 'Geeks', 'age':22}

# Using del to remove an item
del d["age"]
print(d)

# Using pop() to remove an item and return the value
val = d.pop(1)
print(val)

# Using popitem to removes and returns
# the last key-value pair.
key, val = d.popitem()
print(f"Key: {key}, Value: {val}")

# Clear all items from the dictionary
d.clear()
print(d)

# {1: 'Geeks', 2: 'For', 3: 'Geeks'}
# Geeks
# Key: 3, Value: Geeks
# {}
```


## Iterating Through a Dictionary
```python
d = {1: 'Geeks', 2: 'For', 'age':22}

# Iterate over keys
for key in d:
    print(key)

# Iterate over values
for value in d.values():
    print(value)

# Iterate over key-value pairs
for key, value in d.items():
    print(f"{key}: {value}")
    
# 1
# 2
# age
# Geeks
# For
# 22
# 1: Geeks
# 2: For
# age: 22
```


## Nested Dictionaries
![](https://media.geeksforgeeks.org/wp-content/uploads/Dictionary-Creation-1.jpg)
```python
d = {1: 'Geeks', 2: 'For',
        3: {'A': 'Welcome', 'B': 'To', 'C': 'Geeks'}}

print(d)
# {1: 'Geeks', 2: 'For', 3: {'A': 'Welcome', 'B': 'To', 'C': 'Geeks'}}
```


## Copy Dictionaries in Python
A copy of a dictionary can be created using either **shallow copy** or **deep copy** methods. These methods allow duplicating dictionary objects, but they behave differently when it comes to nested data. Let's discuss both in detail.

### 1. Shallow Copy
A **shallow copy** makes a new dictionary with same outer values as the original. But if the dictionary has nested data (like a list or another dictionary), both copies still share that inner data. So, changes to nested parts will affect other.

It is created using **copy.copy()** method from Python’s copy module.

**Example:**
This code shows that in a shallow copy, changes to nested data affect both the original and the copy because the nested parts are shared.
```python
import copy
original = {'name': 'Alice', 'marks': {'math': 90, 'science': 95}}

# Create a shallow copy
shallow = copy.copy(original)

# Modify nested value in the copy
shallow['marks']['math'] = 100

print("Original:", original)
print("Shallow Copy:", shallow)

# Original: {'name': 'Alice', 'marks': {'math': 100, 'science': 95}}
# Shallow Copy: {'name': 'Alice', 'marks': {'math': 100, 'science': 95}}
```
**Explanation:**
- **shallow = copy.copy(original):** creates a shallow copy, nested '**marks**' remains shared.
- **shallow['marks']['math'] = 100:** updates '**math**' in the shared nested dictionary.
- **print(original), print(shallow):** both show updated '**math**' value due to shared data.

### 2. Deep Copy
A **deep copy** makes a new dictionary and also creates separate copies of all nested data (like lists or other dictionaries). This means original and copy are completely independent, changes made to nested parts do not affect other.

It is created using **copy.deepcopy()** method from Python’s copy module.

**Example:**
This Example shows that a deep copy creates a fully independent copy of both the outer and nested data, so changes in the copy do not affect the original.
```python
import copy
original = {'name': 'Alice', 'marks': {'math': 90, 'science': 95}}

# Create a deep copy
deep = copy.deepcopy(original)

# Modify nested value in the deep copy
deep['marks']['math'] = 100

print("Original:", original)
print("Deep Copy:", deep)

# Original: {'name': 'Alice', 'marks': {'math': 90, 'science': 95}}
# Deep Copy: {'name': 'Alice', 'marks': {'math': 100, 'science': 95}}
```
**Explanation:**
- **deep = copy.deepcopy(original):** creates a deep copy, nested '**marks**' is also copied separately.
- **deep['marks']['math'] = 100:** updates '**math**' in the deep copy’s nested dictionary only.
- **print(original), print(deep):** original remains unchanged, only deep copy shows the updated '**math**' value.










