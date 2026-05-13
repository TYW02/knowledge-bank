https://www.geeksforgeeks.org/python/python-tuples/
#Tuple

A tuple in Python is an immutable ordered collection of elements.

- Tuples are similar to lists, but unlike lists, they **cannot be changed** after their creation (i.e., they are immutable).
- Tuples can hold elements of different data types.
- The main characteristics of tuples are being **ordered** , **heterogeneous** and **immutable**.


## Creating a Tuple
A tuple is created by placing all the items inside parentheses (), separated by commas. A tuple can have any number of items and they can be of different [data types](https://www.geeksforgeeks.org/python/python-data-types/).
```python
tup = ()
print(tup)

# Using String
tup = ('Geeks', 'For')
print(tup)

# Using List
li = [1, 2, 4, 5, 6]
print(tuple(li))

# Using Built-in Function
tup = tuple('Geeks')
print(tup)

# ()
# ('Geeks', 'For')
# (1, 2, 4, 5, 6)
# ('G', 'e', 'e', 'k', 's')
```


## Creating a Tuple with Mixed Datatype
Tuples can contain elements of various data types, including other tuples, [lists](https://www.geeksforgeeks.org/python/python-lists/), [dictionaries](https://www.geeksforgeeks.org/python/python-dictionary/) and even [functions](https://www.geeksforgeeks.org/python/python-functions/).
```python
tup = (5, 'Welcome', 7, 'Geeks')
print(tup)

# Creating a Tuple with nested tuples
tup1 = (0, 1, 2, 3)
tup2 = ('python', 'geek')
tup3 = (tup1, tup2)
print(tup3)

# Creating a Tuple with repetition
tup1 = ('Geeks',) * 3
print(tup1)

# Creating a Tuple with the use of loop
tup = ('Geeks')
n = 5
for i in range(int(n)):
    tup = (tup,)
    print(tup)
    
# (5, 'Welcome', 7, 'Geeks')
# ((0, 1, 2, 3), ('python', 'geek'))
# ('Geeks', 'Geeks', 'Geeks')
# ('Geeks',)
# (('Geeks',),)
# ((('Geeks',),),)
# (((('Geeks',),),),)
# ((((('Geeks',),),),),)
```


# Python Tuple Basic Operations
- Accessing of Python Tuples
- Concatenation of Tuples
- Slicing of Tuple
- Deleting a Tuple

## Accessing of Tuples
We can access the elements of a tuple by using indexing and [slicing](https://www.geeksforgeeks.org/python/tuple-slicing-python/), similar to how we access elements in a list. Indexing starts at 0 for the first element and goes up to n-1, where n is the number of elements in the tuple. Negative indexing starts from -1 for the last element and goes backward.
```python
# Accessing Tuple with Indexing
tup = tuple("Geeks")
print(tup[0])

# Accessing a range of elements using slicing
print(tup[1:4])  
print(tup[:3])

# Tuple unpacking
tup = ("Geeks", "For", "Geeks")

# This line unpack values of Tuple1
a, b, c = tup
print(a)
print(b)
print(c)

# G
# ('e', 'e', 'k')
# ('G', 'e', 'e')
# Geeks
# For
# Geeks
```


## Concatenation of Tuples
Tuples can be concatenated using the + operator. This operation combines two or more tuples to create a new tuple.
![](https://media.geeksforgeeks.org/wp-content/uploads/Tuple-Concatenation-1.jpg)

```python
tup1 = (0, 1, 2, 3)
tup2 = ('Geeks', 'For', 'Geeks')

tup3 = tup1 + tup2
print(tup3)

# (0, 1, 2, 3, 'Geeks', 'For', 'Geeks')
```


## Slicing of Tuple
[Slicing a tuple](https://www.geeksforgeeks.org/python/tuple-slicing-python/) means creating a new tuple from a subset of elements of the original tuple. The slicing syntax is tuple[start:stop:step].
![](https://media.geeksforgeeks.org/wp-content/uploads/Slicing-of-Tuple-1.jpg)

```python
tup = tuple('GEEKSFORGEEKS')

# Removing First element
print(tup[1:])

# Reversing the Tuple
print(tup[::-1])

# Printing elements of a Range
print(tup[4:9])

# ('E', 'E', 'K', 'S', 'F', 'O', 'R', 'G', 'E', 'E', 'K', 'S')
# ('S', 'K', 'E', 'E', 'G', 'R', 'O', 'F', 'S', 'K', 'E', 'E', 'G')
# ('S', 'F', 'O', 'R', 'G')
```


## Deleting a Tuple
Since tuples are immutable, we cannot delete individual elements of a tuple. However, we can delete an entire tuple using [del statement](https://www.geeksforgeeks.org/python/python-del-to-delete-objects/).
```python
tup = (0, 1, 2, 3, 4)
del tup
```


## Tuple Unpacking with Asterisk (`*`)
In Python, the ****" * "**** operator can be used in tuple unpacking to grab multiple items into a list. 
This is useful when you want to extract just a few specific elements and collect the rest together.
```python
tup = (1, 2, 3, 4, 5)

a, *b, c = tup

print(a) 
print(b) 
print(c)
# 1
# [2, 3, 4]
# 5
```
**Explanation:**
- **a** gets the first item.
- **c** gets the last item.
- **b** collects everything in between into a list.





































