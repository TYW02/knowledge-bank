#Sets
https://www.geeksforgeeks.org/python/python-sets/

Python set is an **unordered collection** of multiple items having different datatypes. In Python, sets are **mutable**, **unindexed** and do not contain duplicates. The order of elements in a set is not preserved and can change.


## Creating a Set in Python
```python
set1 = {1, 2, 3, 4}
print(set1)
# {1, 2, 3, 4}
```


### Using the Set() Function
```python
set1 = set()
print(set1)

set1 = set("GeeksForGeeks")
print(set1)

# Creating a Set with the use of a List
set1 = set(["Geeks", "For", "Geeks"])
print(set1)

# Creating a Set with the use of a tuple
tup = ("Geeks", "for", "Geeks")
print(set(tup))

# Creating a Set with the use of a dictionary
d = {"Geeks": 1, "for": 2, "Geeks": 3}
print(set(d))

# set()
# {'e', 'r', 'o', 'k', 'G', 's', 'F'}
# {'For', 'Geeks'}
# {'for', 'Geeks'}
# {'for', 'Geeks'}
```


## Unordered, Unindexed and Mutability
In set, the order of elements is not guaranteed to be the same as the order in which they were added. The output could vary each time we run the program. Also the duplicate items entered are removed by itself.

We can add elements to the set using **add()**. We can remove elements from the set using **remove()**. The set changes after these operations, demonstrating its mutability. However, we cannot changes its items directly.
```python
set1 = {3, 1, 4, 1, 5, 9, 2}

print(set1)  # Output may vary: {1, 2, 3, 4, 5, 9}

# Unindexed: Accessing elements by index is not possible
# This will raise a TypeError
try:
    print(set1[0])
except TypeError as e:
    print(e)
    
# {1, 2, 3, 4, 5, 9}
# 'set' object is not subscriptable
```


## Adding Elements to a Set in Python
We can add items to a set using [add() method](https://www.geeksforgeeks.org/python/set-add-python/) and [update() method](https://www.geeksforgeeks.org/python/python-set-update/). 
add() method can be used to add only a single item. 
To add multiple items we use update() method.
```python
# Creating a set
set1 = {1, 2, 3}

# Add one item
set1.add(4)

# Add multiple items
set1.update([5, 6])

print(set1)
# {1, 2, 3, 4, 5, 6}
```


## Accessing a Set in Python
We can loop through a set to access set items as set is unindexed and do not support accessing elements by indexing. 
Also we can use [in keyword](https://www.geeksforgeeks.org/python/python-in-keyword/) which is membership operator to check if an item exists in a set.
```python
set1 = set(["Geeks", "For", "Geeks."])

# Accessing element using For loop
for i in set1:
    print(i, end=" ")

# Checking the element# using in keyword
print("Geeks" in set1)

# Geeks For Geeks. True
```
**Explanation:**
- This loop will print each item in the set. Since sets are unordered, the order of items printed is not guaranteed.
- This code checks if "Geeks" is in set1 and prints a corresponding message.


## Removing Elements from the Set in Python
We can remove an element from a set in Python using several methods: remove(), discard() and pop(). Each method works slightly differently :
- Using [remove() Method](https://www.geeksforgeeks.org/python/python-remove-discard-sets/) or [discard() Method](https://www.geeksforgeeks.org/python/python-set-discard-function/)
- Using [pop() Method](https://www.geeksforgeeks.org/python/python-set-pop-method/)
- Using [clear() Method](https://www.geeksforgeeks.org/python/python-set-clear-method/)

### Using remove() Method or discard() Method
- remove() method removes a specified element from the set. If the element is not present in the set, it raises a KeyError. 

- discard() method also removes a specified element from the set. Unlike remove(), if the element is not found, it does not raise an error.
```python
# Using Remove Method
set1 = {1, 2, 3, 4, 5}
set1.remove(3)
print(set1)  

# Attempting to remove an element that does not exist
try:
    set1.remove(10)
except KeyError as e:
    print("Error:", e)  

# Using discard() Method
set1.discard(4)
print(set1)  

# Attempting to discard an element that does not exist
set1.discard(10)  # No error raised
print(set1)

# {1, 2, 4, 5}
# Error: 10
# {1, 2, 5}
# {1, 2, 5}
```


### Using pop() Method
pop() method removes and returns an arbitrary element from the set. This means we don't know which element will be removed. If the set is empty, it raises a KeyError.
```python
set1 = {1, 2, 3, 4, 5}
val = set1.pop()
print(val)
print(set1)

# Using pop on an empty set
set1.clear()  # Clear the set to make it empty
try:
    set1.pop()
except KeyError as e:
    print("Error:", e)
    
# 1
# {2, 3, 4, 5}
# Error: 'pop from an empty set'
```


### Using clear() Method
```python
set1 = {1, 2, 3, 4, 5}
set1.clear()
print(set1)
# set()
```


## Frozen Sets in Python
A [frozenset](https://www.geeksforgeeks.org/python/frozenset-in-python/) in Python is a built-in data type that is similar to a set but with one key difference that is immutability. This means that once a frozenset is created, we cannot modify its elements that is we cannot add, remove or change any items in it. Like regular sets, a frozenset cannot contain duplicate elements.

If no parameters are passed, it returns an empty frozenset.
```python
# Creating a frozenset from a list
fset = frozenset([1, 2, 3, 4, 5])
print(fset)  

# Creating a frozenset from a set
set1 = {3, 1, 4, 1, 5}
fset = frozenset(set1)
print(fset)

# frozenset({1, 2, 3, 4, 5})
# frozenset({1, 3, 4, 5})
```


## Typecasting Objects into Sets
Typecasting objects into sets in Python refers to converting various data types into a set. Python provides the set() constructor to perform this typecasting, allowing us to convert lists, tuples and strings into sets.
```python
# Typecasting list into set
li = [1, 2, 3, 3, 4, 5, 5, 6, 2]
set1 = set(li)
print(set1)

# Typecasting string into set
s = "GeeksforGeeks"
set1 = set(s)
print(set1)

# Typecasting dictionary into set
d = {1: "One", 2: "Two", 3: "Three"}
set1 = set(d)
print(set1)

# {1, 2, 3, 4, 5, 6}
# {'f', 'G', 's', 'k', 'r', 'e', 'o'}
# {1, 2, 3}
```


# Advantage of Set in Python
- **Unique Elements**: Sets can only contain unique elements, so they can be useful for removing duplicates from a collection of data.
- **Fast Membership Testing**: Sets are optimized for fast membership testing, so they can be useful for determining whether a value is in a collection or not.
- **Mathematical Set Operations:** Sets support mathematical set operations like union, intersection and difference, which can be useful for working with sets of data.
- **Mutable**: Sets are mutable, which means that you can add or remove elements from a set after it has been created.


# Disadvantage of Sets in Python
- **Unordered**: Sets are unordered, which means that you cannot rely on the order of the data in the set. This can make it difficult to access or process data in a specific order.
- **Limited Functionality:** Sets have limited functionality compared to lists, as they do not support methods like append() or pop(). This can make it more difficult to modify or manipulate data stored in a set.
- **Memory Usage:** Sets can consume more memory than lists, especially for small datasets. This is because each element in a set requires additional memory to store a hash value.
- **Less Commonly Used:** Sets are less commonly used than lists and dictionaries in Python, which means that there may be fewer resources or libraries available for working with them. This can make it more difficult to find solutions to problems or to get help with debugging.

Overall, sets can be a useful data structure in Python, especially for removing duplicates or for fast membership testing. However, their lack of ordering and limited functionality can also make them less versatile than lists or dictionaries, so it is important to carefully consider the advantages and disadvantages of using sets when deciding which data structure to use in your Python program.


# Set Method in Python
|Function|Description|
|---|---|
|[add()](https://www.geeksforgeeks.org/python/set-add-python/)|Adds an element to a set|
|[remove()](https://www.geeksforgeeks.org/python/python-remove-discard-sets/)|Removes an element from a set. If the element is not present in the set, raise a KeyError|
|[clear()](https://www.geeksforgeeks.org/python/python-set-clear-method/)|Removes all elements form a set|
|[copy()](https://www.geeksforgeeks.org/python/set-copy-python/)|Returns a shallow copy of a set|
|[pop()](https://www.geeksforgeeks.org/python/python-set-pop-method/)|Removes and returns an arbitrary set element. Raise KeyError if the set is empty|
|[update()](https://www.geeksforgeeks.org/python/python-set-update/)|Updates a set with the union of itself and others|
|[union()](https://www.geeksforgeeks.org/python/union-function-python/)|Returns the union of sets in a new set|
|[difference()](https://www.geeksforgeeks.org/python/python-set-difference/)|Returns the difference of two or more sets as a new set|
|[difference_update()](https://www.geeksforgeeks.org/python/python-set-difference_update/)|Removes all elements of another set from this set|
|[discard()](https://www.geeksforgeeks.org/python/python-remove-discard-sets/)|Removes an element from set if it is a member. (Do nothing if the element is not in set)|
|[intersection()](https://www.geeksforgeeks.org/python/intersection-function-python/)|Returns the intersection of two sets as a new set|
|[intersection_update()](https://www.geeksforgeeks.org/python/python-set-intersection_update-method/)|Updates the set with the intersection of itself and another|
|[isdisjoint()](https://www.geeksforgeeks.org/python/python-set-isdisjoint-method/)|Returns True if two sets have a null intersection|
|[issubset()](https://www.geeksforgeeks.org/python/python-set-issubset-method/)|Returns True if another set contains this set|
|[issuperset()](https://www.geeksforgeeks.org/python/issuperset-in-python/)|Returns True if this set contains another set|
|[symmetric_difference()](https://www.geeksforgeeks.org/python/python-set-symmetric_difference-2/)|Returns the symmetric difference of two sets as a new set|
|[symmetric_difference_update()](https://www.geeksforgeeks.org/python/python-set-symmetric-difference-update/)|Updates a set with the symmetric difference of itself and another|
