#String 

A string is a sequence of characters. Python treats anything inside quotes as a string. This includes letters, numbers, and symbols. Python has no character data type so single character is a string of length 1.
```python
s = "GfG"

print(s[1]) # access 2nd char
s1 = s + s[0] # update
print(s1) # print

# f
# GFGG
```
- In this example, s holds the value "GFG" and is defined as a string

## Creating a String
Strings can be created using either **single (')** or **double (")** quotes.
```python
s1 = 'GfG'
s2 = "GfG"
print(s1)
print(s2)
```



## Multi-line Strings
If we need a string to span multiple lines then we can use **triple quotes (''' or """)**.
```python
s = """I am Learning
Python String on GeeksforGeeks"""
print(s)

s = '''I'm a 
Geek'''
print(s)

# I am Learning
# Python String on GeeksforGeeks
# I'm a 
# Geek
```


## Accessing Characters in Python String

Strings in Python are sequences of characters, so we can access individual characters using **indexing.** Strings are indexed starting from **0** and **-1** from end. This allows us to retrieve specific characters from the string.
![[frame_3086.webp]]
```python
s = "GeeksforGeeks"

# Accesses first character: 'G'
print(s[0])  

# Accesses 5th character: 's'
print(s[4])

# G
# s
```


# String Slicing
#Slicing 
[Slicing](https://www.geeksforgeeks.org/python/string-slicing-in-python/) is a way to extract portion of a string by specifying the **start** and **end** indexes. The syntax for slicing is **string[start:end]**, where **start** starting index and **end** is stopping index (excluded).
```python
s = "GeeksforGeeks"

# Retrieves characters from index 1 to 3: 'eek'
print(s[1:4])  

# Retrieves characters from beginning to index 2: 'Gee'
print(s[:3])   

# Retrieves characters from index 3 to the end: 'ksforGeeks'
print(s[3:])   

# Reverse a string
print(s[::-1])

# eek
# Gee
# ksforGeeks
# skeeGrofskeeG
```


## String Immutability
**Strings in Python are immutable**. This means that they cannot be changed after they are created. If we need to manipulate strings then we can use methods like **concatenation, slicing,** or **formatting** to create new strings based on the original.
```python
s = "geeksforGeeks"

# Trying to change the first character raises an error
# s[0] = 'I'  # Uncommenting this line will cause a TypeError

# Instead, create a new string
s = "G" + s[1:]
print(s)

# GeeksforGeeks
```


## Deleting a String
In Python, it is not possible to delete individual characters from a string since strings are immutable. However, we can delete an entire string variable using the [**del**](https://www.geeksforgeeks.org/python/python-del-to-delete-objects/) keyword.
```python
s = "GfG"

# Deletes entire string
del s
```


## Updating a String
To update a part of a string we need to create a new string since strings are immutable
```python
s = "hello geeks"

# Updating by creating a new string
s1 = "H" + s[1:]

# replacnig "geeks" with "GeeksforGeeks"
s2 = s.replace("geeks", "GeeksforGeeks")
print(s1)
print(s2)

# Hello geeks
# hello GeeksforGeeks
```

Explanation:
- **For s1,** The original string **s** is sliced from index 1 to end of string and then concatenate "H" to create a new string **s1**.
- **For s2,** we can created a new string s2 and used [replace() method](https://www.geeksforgeeks.org/python/python-string-replace/) to replace 'geeks' with 'GeeksforGeeks'.

## Common String Methods

**len()**: The [len()](https://www.geeksforgeeks.org/python/python-len-function/) function returns the total number of characters in a string.
```python
s = "GeeksforGeeks"
print(len(s))

# output: 13
```

**upper() and lower()**: [upper()](https://www.geeksforgeeks.org/python/python-string-upper/) method converts all characters to uppercase. [lower()](https://www.geeksforgeeks.org/python/python-string-lower/) method converts all characters to lowercase.
```python
s = "Hello World"

print(s.upper())   # output: HELLO WORLD

print(s.lower())   # output: hello world
```


**strip() and replace()**: [strip()](https://www.geeksforgeeks.org/python/python-string-strip/) removes leading and trailing whitespace from the string and [replace(old, new)](https://www.geeksforgeeks.org/python/python-string-replace/) replaces all occurrences of a specified substring with another.
```python
s = "   Gfg   "

# Removes spaces from both ends
print(s.strip())    

s = "Python is fun"

# Replaces 'fun' with 'awesome'
print(s.replace("fun", "awesome"))
```

## Concatenating and Repeating Strings
We can concatenate strings using [+ operator](https://www.geeksforgeeks.org/python/python-operators/) and repeat them using [* operator](https://www.geeksforgeeks.org/python/python-operators/).

Strings can be combined by using **+ operator**.
```python
s1 = "Hello"
s2 = "World"
s3 = s1 + " " + s2
print(s3)
# Hello World
```


We can repeat a string multiple times using * operator.
```python
s = "Hello "
print(s * 3)
# Hello Hello Hello
```


## Formatting Strings


### F-Strings
```python
name = "Alice"
age = 22
print(f"Name: {name}, Age: {age}")
# Name: Alice, Age: 22
```


### Using format()
```python
s = "My name is {} and I am {} years old.".format("Alice", 22)
print(s)
# My name is Alice and I am 22 years old.
```






