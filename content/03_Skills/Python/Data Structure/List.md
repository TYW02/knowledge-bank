#List 
https://www.geeksforgeeks.org/python/python-lists/
In Python, a **list** is a built-in dynamic sized array (automatically grows and shrinks). We can store all types of items (including another list) in a list.

- Can contain duplicate items.
- Mutable : We can modify, replace or delete the items.
- Ordered : Maintains the order of elements based on how they are added.
- Items can be accessed directly using their position (index), starting from 0.
- May contain mixed type of items, this is possible because a list mainly stores references at contiguous locations and actual items maybe stored at different locations.
```python
# Creating a Python list with different data types
a = [10, 20, "GfG", 40, True]
print(a)

# Accessing elements using indexing
print(a[0])  # 10
print(a[1])  # 20
print(a[2])  # "GfG"
print(a[3])  # 40
print(a[4])  # True

# Checking types of elements
print(type(a[2]))  # str
print(type(a[4]))  # bool
```


## Creating a List

### Using Square Brackets
```python
# List of integers
a = [1, 2, 3, 4, 5]

# List of strings
b = ['apple', 'banana', 'cherry']

# Mixed data types
c = [1, 'hello', 3.14, True]

print(a)
print(b)
print(c)

# [1, 2, 3, 4, 5]
# ['apple', 'banana', 'cherry']
# [1, 'hello', 3.14, True]
```


### Using list() Constructor
We can also create a list by passing an **iterable** (like a [****string****](https://www.geeksforgeeks.org/python/python-string/), [****tuple****](https://www.geeksforgeeks.org/python/tuples-in-python/) or another ****list****) to [****list()**** function](https://www.geeksforgeeks.org/python/list-constructor-in-python/).
```python
# From a tuple
a = list((1, 2, 3, 'apple', 4.5))  
print(a)

# [1, 2, 3, 'apple', 4.5]
```


## Accessing List Elements
Elements in a list can be accessed using **indexing**. Python indexes start at **0**, so **a[0]** will access the first element, while **negative indexing** allows us to access elements from the end of the list. Like index -1 represents the last elements of list.
```python
a = [10, 20, 30, 40, 50]

# Access first element
print(a[0])    

# Access last element
print(a[-1])
```


## Adding Elements into List
#Append #Extend #Insert 
- [**append():**](https://www.geeksforgeeks.org/python/python-list-append-method/) Adds an element at the end of the list.
- [**extend():**](https://www.geeksforgeeks.org/python/python-list-extend-method/) Adds multiple elements to the end of the list.
- [**insert()**](https://www.geeksforgeeks.org/python/python-list-insert/)****:**** Adds an element at a specific position.
```python
# Initialize an empty list
a = []

# Adding 10 to end of list
a.append(10)  
print("After append(10):", a)  

# Inserting 5 at index 0
a.insert(0, 5)
print("After insert(0, 5):", a) 

# Adding multiple elements  [15, 20, 25] at the end
a.extend([15, 20, 25])  
print("After extend([15, 20, 25]):", a)

# After append(10): [10]
# After insert(0, 5): [5, 10]
# After extend([15, 20, 25]): [5, 10, 15, 20, 25]
```


### Updating Elements into List
```python
a = [10, 20, 30, 40, 50]

# Change the second element
a[1] = 25 
print(a)
# [10, 25, 30, 40, 50]
```


### Removing Elements from List
- [**remove()**](https://www.geeksforgeeks.org/python/python-list-remove/)****:**** Removes the first occurrence of an element.
- [**pop()**](https://www.geeksforgeeks.org/python/python-list-pop-method/)****:**** Removes the element at a specific index or the last element if no index is specified.
- [**del statement**](https://www.geeksforgeeks.org/python/python-del-to-delete-objects/)****:**** Deletes an element at a specified index.
```python
a = [10, 20, 30, 40, 50]

# Removes the first occurrence of 30
a.remove(30)  
print("After remove(30):", a)

# Removes the element at index 1 (20)
popped_val = a.pop(1)  
print("Popped element:", popped_val)
print("After pop(1):", a) 

# Deletes the first element (10)
del a[0]  
print("After del a[0]:", a)

# After remove(30): [10, 20, 40, 50]
# Popped element: 20
# After pop(1): [10, 40, 50]
# After del a[0]: [40, 50]
```


## Iterating Over Lists
We can iterate the Lists easily by using a [**for loop**](https://www.geeksforgeeks.org/python/loops-in-python/) or other iteration methods. Iterating over lists is useful when we want to do some operation on each item or access specific items based on certain conditions. Let's take an example to iterate over the list using **for loop**.

```python
a = ['apple', 'banana', 'cherry']

# Iterating over the list
for item in a:
    print(item)
    
# apple
# banana
# cherry
```


## Nested Lists in Python
A nested list is a list within another list, which is useful for representing matrices or tables. We can access nested elements by chaining indexes.
```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access element at row 2, column 3
print(matrix[1][2])

# 6
```


### Using enumerate()
#enumerate
We can also use the [**enumerate()**](https://www.geeksforgeeks.org/python/enumerate-in-python/) function to iterate through the list. This method provides both the **index (i)** and the **value (val)** of each element during the loop.
```python
a = [1, 3, 5, 7, 9]

# Here, i and val reprsents index and value respectively
for i, val in enumerate(a):
    print (i, val)
    
# 0 1
# 1 3
# 2 5
# 3 7
# 4 9
```


## List Comprehension

Making a list of first 10 cubes:
```python
cubes = [value**3 for value in range(1, 11)]
```

List comprehension combines the for loop & creation of a new element into 1 line.

## Slicing List
#Slicing 

```python
foods = ["pizza", "falafel", "carrot cake", "cannotli", "ice cream"]

# To get first 3 in list
for food in foods[:3]:
	print(food)
	
# Middle 3
for food in foods[1:-1]:
	print(food)
	
# Last 3
for food in foods[-3:]:
	print(food)
```


```python
foods[0:3] # this will return index 0, 1, 2
foods[:4] # while this will return from start to index 3
```


## Copying List
#Copy

```python
friend_food = foods[:] # This will make a copy

friend_food = foods # This will not work, any changes made will affect both list
```











