---
title: Function Design
tags:
  - Functions
---
# Determine what you want your function to do

Example: Function to count the vowels of any string and return result as integer

# List the steps of your function 
> [!Example]
> Step 1: Count the vowels in any given string and return an ineger
> Step 2: If the argument is not of type string, raise a TypeError that includes the type that the user passed in.
> Step 3: The vowels that will be included are "aeiouAEIOU". Make sure to handle both uppercase and lowercase. This will be stored as a variable called "vowels" for clarity.
> Step 4: Create a comprehension to count all the vowel occurrences. This list comprehension will be wrapped by the built-in "sum()" function. Which will be returned as an integer


# Think of meaningful name for function

```python 
def count_vowels(text: str) -> int:
	
```

This is a good name because it is simple concise and straight to the point.
Give variable meaningful names and type annotations for clarity.

# Actually code the function
```python
def count_vowels(text: str) -> int:
	if not isinstance(text, str):
		raise TypeError(f'"text" must be a str. "{type(text)}" is invalid.')
		
	vowels: str = 'aeiouAEIOU'
	return sum(1 for letter in text if letter in vowels)
```

Make the logic as simple as you can.
If your function does more than 1 job, consider creating a class that has several methods instead.

Readability is better than cool 1 liners.

# Break the function with all forms of input
```python
from pathlib import Path

def count_vowels(text: str) -> int:
	if not isinstance(text, str):
		raise TypeError(f'"text" must be a str. "{type(text)}" is invalid.')
		
	vowels: str = 'aeiouAEIOU'
	return sum(1 for letter in text if letter in vowels)
	
inputs: dict = {
	'He is over there!': 6,
	'': 0,
	'aeiouAEIOU': 10,
	'aEiOuY': 5,
	True: TypeError,
	Path('text.txt'): TypeError,
}

for var, result in inputs.items():
	try:
		passed: bool = count_vowels(var) == result
		print(f''count_vowels({repr(var)}) == {result}, {passed=}')
	except TypeError as e:
		passed = result is type(e)
		print(f''count_vowels({repr(var)}) == {result}, {passed=}')
```


# Add docstring
Should explain the function and contain a few examples
```python
from pathlib import Path

def count_vowels(text: str) -> int:
"""Counts the number of vowels (A, E, I, O, U, case-insensitive)
in a given string (exluding y & Y).

Examples:
>>> count_vowels('Hello World')
3
>>> count_vowels('AEIOUaeiou')
10
>>> count_vowels('')
0
"""
	if not isinstance(text, str):
		raise TypeError(f'"text" must be a str. "{type(text)}" is invalid.')
		
	vowels: str = 'aeiouAEIOU'
	return sum(1 for letter in text if letter in vowels)
	
inputs: dict = {
	'He is over there!': 6,
	'': 0,
	'aeiouAEIOU': 10,
	'aEiOuY': 5,
	True: TypeError,
	Path('text.txt'): TypeError,
}

for var, result in inputs.items():
	try:
		passed: bool = count_vowels(var) == result
		print(f''count_vowels({repr(var)}) == {result}, {passed=}')
	except TypeError as e:
		passed = result is type(e)
		print(f''count_vowels({repr(var)}) == {result}, {passed=}')
```
