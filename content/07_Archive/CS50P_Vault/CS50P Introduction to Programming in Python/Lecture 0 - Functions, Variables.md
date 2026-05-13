-------
Python Program: [[Hello.py]], [[Calculator.py]]
Topics Covered: #Functions #Arguments #Bugs #Return_Value #Variables #Comments #Pseudocode
Current Status: 
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox"> | |
> | Completed | <input type="checkbox" checked> | |  
> > 

Youtube Link: [Here](https://www.youtube.com/watch?v=JP7ITIXGpHk&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=2&t=158s)

#### [[Lecture 1 - Conditionals|Next Lecture]]
---
## Functions
- What is a Function
	- Like an action or verb that lets you do something in a program.
	- 

- Predetermined Functions
	- Generally speaking most languages come with a set of predetermined functions.
---



---
## Arguments
- What is an Argument
	- An input to a functions to influnces its behavior
---


---
## Bugs
- What are bugs
	- A mistake in a program
	- Can take many form
---


---
## Return Values
- What does return value do ?
	- Get the user's input and hand it back to the programmer
---


---
## Variables
- What is a variable
	- Variable can store a value, number, text even images or videos.
	- A Variable is just a container for some value inside of a computer 


Variables are stored in the computer's memory

---





---
## Comments
- What is a Comment
	- Comments are notes to yourself in your code 

To comment in Python --> #

- To Multi-line comment in Python 
```python
"""
This is a comment
"""
```
	

- What is the purpose of Commenting
	- To remind yourself what you are trying to accomplish with the code
	- And whenever a bug occurs you can read the intention of your code to see if it is accomplishing its job



## Pseudocode
- What is Pseudocode
	- Using english to express your thoughts 

- Purpose of Pseudocode
	- Allows you to outline your progrom in advance 
	- Helps you stucture your to-do list
	- Very useful especially when you have no idea how to write the code

Breaks a bigger program down into small bite size tasks


---








---





---



---




---
## Parameters
- What is a Parameter
	- What you pass to a function

---




---
## Arguments
- What are Argument
	- When you use the function and pass in values those inputs are arguments

 ---

---



---
## Parameters
- What are the 2 types of Parameters
	- Positional Parameters
		- The 1st thing you pass to print gets printed first, 2nd thing 2nd ....
	- Named Parameters
		- They are optional
		- sep, end

--- 



---
## Escape Character
 - Something that you can't just type it once, you need to express it with multiple characters

---





---
## Print()

- Arguments
	- Takes multiple arguments if you seperate the argument is a , 

When you pass multiple arguments to print it auto spaces for you
	- See [[Hello.py#Multi argument print|Here]]

Autmatically prints on the next line


## Documents
Find [Link](https://docs.python.org/3/library/functions.html#print) here.



## Parameters
print(\*objects, _sep=' '_, _end='\\n'_, _file=None_, _flush=False_)

\*objects --> means print can take any number of objects
sep=' ' --> seperator, if you pass multiple arguments to print it defaults to printing a space
end='\\n' --> new line


---




---
## Strings (str)
#String


- Type of data

## Documentation
Click [Here](https://docs.python.org/3/library/string.html)


## .strip()
- What does it do ?
	- Removes any leading (spaces at the beginning) and trailing (spaces at the end) characters

### Syntax
```python 
string.strip(characters)
```

### Code Examples and Documents
Click [[Hello.py#^4b0f17|Code Examples]]

Click [Documents](https://www.w3schools.com/python/ref_string_strip.asp)


## .capitalize()
- What does it do ?
	- Returns a copy of the original string and converts the first character of the string to a capital letter, while making all other characters in the string **lowercase** letters

### Syntax
```python
string_name.capitalize()
```

### Code Examples and Documents
Click [[Hello.py#^0298c8|Code Examples]] 

Click [Documents](https://www.geeksforgeeks.org/string-capitalize-python/)



## .title()
- What does it do ?
	- Returns a string where the first character in every word is upper case. Like a header, or a title
	- If the word contains a number or a symbol, the first letter after that will be converted to upper case.

### Syntax
```python
string.title()
```


### Code Examples and Documents
Click [[Hello.py#Using .title() for User input|Code Examples]]

Click [Documents](https://www.w3schools.com/python/ref_string_title.asp)




## .split()
- What does it do ?
	- It returns a sequence of values
	- Splits a string into a list

### Syntax
```python
string.split(separator, maxsplit)
```


### Parameter Values
| Parameter | Description |
| ---- | ---- |
| *separator* | Optional. Specifies the separator to use when splitting the string. By default any whitespace is a separator |
| *maxsplit* | Optional. Specifies how many splits to do. Default value is -1, which is "all occurrences" |


### Code Examples and Documents
Click [[Hello.py#.split()|Code Examples]]

Click [Documents](https://www.w3schools.com/python/ref_string_split.asp)









### Format String / f-string
- What is the purpose of f-string
	- The idea behind f-strings is to make string interpolation simpler.

- How to create a f-string
	- Prefix the string with the letter "f".

F-Strings provide a concise and convenient way to embed python expressions inside string literals for formatting.

## Code Example
Click
[[Hello.py#^6f074c|Hello.py]]
[[Calculator.py#f-string (Adding , every 000)|Calculator.py]]


## Documentation
Click [Here](https://www.geeksforgeeks.org/formatted-string-literals-f-strings-python/)

 ---






---
# Integer (int)
#Integer

- Type of data
- Only whole numbers
- No decimal points


## Arithmetic Operators

\+ --> Addition
\ - --> Subtraction
\ * --> Multiplication
\ / --> Division
\ % --> Modulo (Gives remainder after dividing 1 number by the next)







----





---
# Converting String to Integer
#String #Integer 

In python a string can be converted into an integer using the built-in *int()* function.

The *int()* function takes in any python data type and converts it into a integer.

## Syntax
```python
int(string)
```


## Documents
Click [[Calculator.py#Converting String to integer|Code Example]]

Click [Documents](https://www.geeksforgeeks.org/convert-string-to-integer-in-python/)


---




---
# Float
#Float

- Type of data
Converts integers into a floating point number

## Syntax
```python
float(value)
```


## Parameter Values
| Parameter | Description |
| ---- | ----|
| *value* | A number or a string that can be converted into a floating point number |


## Documents
Click [[Calculator.py#Float() input|Code Example]]

Click [Documents](https://www.w3schools.com/python/ref_func_float.asp)


# round()
#Float 

- What does it do ?
	- Returns *number* rounded to *ndigits* precision after the decimal point.
	- If *ndigits* is omitted or is **None**, it returns the nearest integer to its input.


## Syntax
```python
round(number[, ndigits])
```
[, ndigits]
- the [ ] just means that the parameter is optional.
- The number of digits you want to round to.


## Documents
Click 

Click [Documents](https://docs.python.org/3/library/functions.html#round)







---





---
# Define (def)
#Define 

- What is it used for ?
	- Used to define a function, it is placed before a function name that is provided by the user to create a user-defined function.

## Syntax
```python
def function_name:
	function definition statements...
```


### Use of def keyword:
- In the case of classes, the def keyword is used for defining the mthods of a class.
- def keywords is also required to define the special member of a class like \_\_init\_\_()
- Provides code reusability rather than writing the code again and again.



## Documents
Click [[Hello.py#Creating function|Code Example]]

Click [Documents](https://www.geeksforgeeks.org/python-def-keyword/)


----





# Scope
- What is scope ?
	- Scope refers to a variable only existing in the context in which you defined it.

### Example
```python
def main():
	name = input("What's your name? ")
	hello()

def hello(to="world"):
	print("hello,", name)

main()


> Output: Error
```

- Name in the main function, you can only use that variable in the name function.
- You cannot use it in the main function, as it doens't exist in the scope

---





---
# Return
- What does it do ?
	- Return a value explicitly to yourself
	- Used to end the execution of the function call and "returns" the result to the caller.

> [!INFO]
> **Note**: *Return statement can not be used outside the function*

## Syntax
```python
def fun():
	statements
	.
	.
	return [expression]
```
 

## Documents
Click [[Calculator.py#Using Return|Code Example]]

Click [Documents](https://www.geeksforgeeks.org/python-return-statement/)







---