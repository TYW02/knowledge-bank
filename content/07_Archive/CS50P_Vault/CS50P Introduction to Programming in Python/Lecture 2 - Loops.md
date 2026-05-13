----
Python Program: [[hogwarts.py]] [[mario.py]] [[cat.py]] 
Topic Covered:
Current Status:
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox" > | |
> | Completed | <input type="checkbox" checked> | |  
> 

Youtube Link: [Here](https://www.youtube.com/watch?v=-7xg8pGcP6w&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=5&t=4s)

----
# while Loop

Is a construct that allows you to ask a question again and again.

With the ==while== loop we can execute a set of statements as long as a condition is true.

### Syntax
```python
i = 1
while i < 6:
	print(i)
	i += 1
```

> [!INFO]
> **Note**: Remember to increment i, or else the loop will continue forever.

The ==while== loop requires relevant variables to be ready, in this example we need to define an indexing variable ==i==, which we set to 1.


### Documents
Click [[cat.py|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_while_loops.asp)

----


# List
#List
- What are lists ?
	- They are used to store multiple items in a single variable.
	- Built-in data types

Lists are created using square brackets:

## Syntax
```python
thislist = ["apple", "banana", "cherry"]
print(thislist)
```


## List Items
- List items are ordered, changeable, and allow duplicate values.
- List items are indexed, the first item has index [0] , and the second item has index [1] etc.


### Ordered
- When we say that lists are ordered, it means that the items have a defined order, and that order will not change.

- If you add new items to a list, the new items will be placed at the end of the list.
> [!INFO]
> **Note**: There are some _list methods_ that will change the order, but in general: the order of the items will not change.


### Changeable
- The list is changeable, meaning that we can change, add, and remove items in a list after it has been created.



### Allow Duplicates
- Since lists are indexed, lists can have items with the same value:
```python
thislist = ["apple", "banana", "cherry", "apple", "cherry"]
```

## Documents
Click [[cat.py#Using for loop|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_lists.asp)

----





----
# for Loop
- What is it used for ?
	- A for loop is used for iterating over a sequence (list, tuple, dictionary, set, string)
	- With the for loop we can execute a set of statements, once for each item in a list, tuple, set etc.

## Syntax
```python
fruits = ["apple", "banana", "cherry"]
for x in fruits:
	print(x)

```

The for loop does not require an indexing variable to set beforehand.


### Documents
Click [[cat.py#Using for loop|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_for_loops.asp)

----





----
# range()
- What is the purpose of it ?
	- Returns a sequence of numbers, starting from 0 by default, and increments by 1 (by default), and stops before a specified number.


## Syntax
```python
range(start, stop, step)
```


## Parameter Values
| Parameter | Description                                                                       |
| --------- | --------------------------------------------------------------------------------- |
| *start*   | Optional. An integer number specifying at which position to start. Default is 0   |
| *stop*    | Required. An interger number specifying at which position to stop (not included). |
| *step*    | Optional. An integer number specifying the incrementation. Default is 1                                                                                  |


## Documents
Click [[cat.py#Using for loop|Code Example]]

Click [Documents](https://www.w3schools.com/python/ref_func_range.asp)

----





# len()
- What does it do ?
	- The len() function returns the number of items in an object
	- When the object is a string, the len() function returns the number of characters in the string.


## Syntex
```python
len(object)
```


## Parameter Values
| Parameter | Description |
| --------- | ----------- |
| *object*  | Required. An Object. Must be a sequence or a collection            |


## Documents
Click [[hogwarts.py#^11c88a|Code Example]]

Click [Documents](https://www.w3schools.com/python/ref_func_len.asp)


----



# Dictionary (dict)
#dict

- Type of data structure
- Used to store data values in key:value pairs
- A dictionary is a collection which is ordered, changeable and do not allow duplicates

> [!INFO]
> As of Python version 3.7, dictionaries are *ordered*. In Pythong 3.6 and earlier, dictionaries are unordered.

- Dictionaries are written with curly brackets, and have keys and values:

## Syntax
```python
thisdict = {"brand": "Ford",
		   "model": "Mustang",
		   "year": 1964
		   }
print(thisdict)
```


## Dictionary Items

- Dictionary items are ordered, changeable, and does not allow duplicates.
- Dictionary items are presented in key:value pairs, and can be referred to by using the key name.

### Example
```python
thisdict = {"brand": "Ford",
		   "model": "Mustang",
		   "year": 1964
		   }
print(thisdict["brand"])
```

## Ordered or Unordered ?
>[!INFO]
>As of Python version 3.7, dictionaries are *ordered*. In Python 3.6 and earlier, dictionaries are *unordered*

When we say that dictionaires are ordered, it means that the items have a defined order, and that order will not change.

Unordered means that the items does not have a defined order, you cannot refer to an item by using an index.


## Changeable

- Dictionaries are changeable, meaning that we can change, add or remove items after the dictionary has been created.


## Duplicates Not Allowed

- Dictionaries cannot have 2 items with the same key:

```python
thisdict = {"brand": "Ford",
		   "model": "Mustang",
		   "year": 1964,
		   "year": 2020
		   }
print(thisdict["brand"])
```

## Documents
Click [[hogwarts.py#Using dict|Code Examples (1)]], [[hogwarts.py#Enhanced Dictionary|Code Example(2)]]

Click [Documents](https://www.w3schools.com/python/python_dictionaries.asp)

----


# None
- What is None ?
	- Used to define a null value, or no value at all.

> [!INFO]
> None is not the same as 0, False, or an empty string.
> None is a data type of its own (NoneType) and only None can be None.

## Syntax 
```python
x = None

print(x)
```

## Documents
Click [[hogwarts.py#Enhanced Dictionary|Code Example]]

Click [Documents](https://www.w3schools.com/python/ref_keyword_none.asp)

----

