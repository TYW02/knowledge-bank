---
title: Testing
tags:
  - PyTest
---
# Testing a Function
```python
# This is the function to be tested
# name_function.py
def get_formatted_name(first, last):
	full_name = f"{first} {last}"
	return full_name.title()
```

```python
from name_function import get_formatted_name
def test_first_last_name():
	formatted_name = get_formatted_name('janis', 'joplin')
	assert formatted_name == 'Janis Joplin'
```
Any function that start with **test_** will be discovered by PyTest

# What is a Unit Test ?
- A unit test verifies that 1 specific aspect of a function's behavior is correct

# What is a Test Case ?
- A collection of unit test that together prove a function behaves as its supposed to, within the full range you expect it to handle.

## A Failing Test
```python
def get_formatted_name(first, middle, last):
	full_name = f"{first} {middle} {last}"
	return full_name.title()
```
When we run pytest, it will fail and return `TypeError: Missing 1 required positional argument: 'last'` 

When responding to a failed test, change function code **NOT** the test code
```python
def get_formatted_name(first, last, middle=""):
	if middle:
		full_name = f"{first} {middle} {last}"
	else:
		full_name = f"{first} {last}"
	return full_name.title()
```


## Adding New Test
```python
def test_first_last_middle_name():
	formatted_name = get_formatted_name('wolfgang', 'mozart', 'amadues')
	assert formatted_name == 'Wolfgang Amadues Mozart'
```

## Using Fixtures
Help in creating reusable and maintainable test code by providing a way to define and manage the setup and teardown logic.
A *Fixture* is a piece of code that runs and returns output before the execution of each test.

```python
@pytest.fixture
def function_name():
	input = value_to_be_passed
	return input
```


### Example
```python
# Importing the math and pytest libraries
import math
import pytest

# Creating the common function for input
@pytest.fixture
def input_value():
   input = 8
   return input

# Creating first test case
def test_check_difference(input_value):
   assert 99-93==input_value

# Creating second test case
def test_check_square_root(input_value):
   assert input_value==math.sqrt(64)
```
In this example `input_value` is used as the input and passed to the input to each test. We have declared 2 test, *test_check_difference*, and *test_check_square_root* that use the value declared by the fixture.

