----
Python Program: [[grade.py]], [[parity.py]], [[house.py]], [[compare.py]], [[]]
Topics Covered: #if #elif #conditionals #match
Current Status: 
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox" > | |
> | Completed | <input type="checkbox" checked> | |  
> > 

Youtube Link: [Here](https://www.youtube.com/watch?v=_b6NgY_pMdw&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=4)

#### [[Lecture 2 - Loops|Next Lecture]]
---


# Conditionals 
- What are conditionals ?
	- Ability to ask questions and answer those questions, in order to decide if you want to execute this line of code or the other. 
	- They allow you to take the proverbial forks in the road

## Syntax
\> --> Greater than
\>= --> Greater than or equal
\< --> Less than
\<= --> Less than or equal
\== --> Equality (Comparing left and right) --> [[compare.py#Using == equal|Example]]
\!= --> Not equals --> [[compare.py#Using != not equal|Example]]

----





----
# If

- What are if statements:
	- If the answer to this question is true, then go ahead and run this code


## Syntax
```python
if b > a:
	print("b is greater than a")
```


## Documents
Click [[compare.py#Comparing x < y and using IF|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_conditions.asp)



## elif
- What are elif statements:
	- The **elif** keyword is pythons way of saying "if the previous conditions were not true, then try this condition"


## Syntax
```python
if b > a:
	print("b is greater than a")
elif a == b:
	print("a and b are equal")
```


## Documents
Click [[compare.py#Using elif|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_conditions.asp)



## else
- What are else statements
	- The **else** keyword catches anything which isn't caught by the preceding conditions

## Syntax
```python
if b > a:  
  print("b is greater than a")  
elif a == b:  
  print("a and b are equal")  
else:  
  print("a is greater than b")
```


## Documents
Click [[compare.py#Using else|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_conditions.asp)


----


## or 
- What does *or* do ?
	- Returns True if one of the statements is true


## Syntax
```python
if (x < y or x > y):
	print("x is not equal to y")
```


## Documents
Click [[compare.py#Using or|Code Examples]]

Click [Documents](https://www.w3schools.com/python/python_operators.asp)


----


## and
- What does it do ?
	- Returns True if both statements are true

## Syntax
```python
if score >= 90 and score <= 100:
	print("Grade: A")
```


## Documents
Click [[grade.py#Using and|Code Examples]]

Click [Documents](https://www.w3schools.com/python/python_operators.asp)


----



## Chaining Comparison Operators
- What does it do ?
	- Checking more than 2 conditions 

## Syntax
```python
if a < b < c:
	...
```


## Documents
Click [[grade.py#Chaining Comparison Operators|Code Example (1)]], [[grade.py#Chaining Comparison Operator (2)|Code Example (2)]]

Click [Documents](https://www.geeksforgeeks.org/chaining-comparison-operators-python/)

----


## bool
- Data Type
- Can only be True or False

- What does it do ?
	- Returns the boolean value of a specified object
	- Will always return True, unless stated

## Syntax
```python
bool(object)
```

## Parameter Values
| Parameter | Description |
| ---- | ----|
| *object* | Any object, like String, List, Number etc.|

## Documents
Click [[parity.py#Writing a function|Code Examples]]

Click [Documents](https://www.w3schools.com/python/ref_func_bool.asp)

----


## Pythonic Expression
There are many ways to solve a certain problem, in the python community of programmers there tend to be some ways that are smiled upon more than other.

## Code Example
Click [[parity.py#Pythonic Expression|Here]]


----



## Match

- Similar to *switch* in other languages


## Syntax 
```python
match variable_name:
	case condition1:
		statment1
	case condition2:
		statment2
	case condition3:
		statment3
	case _:
		statement4
```

> [!INFO]
> Note that *case \_*: is what you want to set the else condition to.



