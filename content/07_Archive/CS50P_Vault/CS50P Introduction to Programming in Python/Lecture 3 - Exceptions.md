----
Python Program: [[number.py]]
Topic Covered: #Exceptions, #TryExcept, #Pass
Current Status:
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox" > | |
> | Completed | <input type="checkbox" checked> | |  

Youtube link: [Here](https://www.youtube.com/watch?v=LW7g1169v7w&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=6)

----

# Exceptions

- What are exceptions ?
	- Exceptions refer to problems in your code.



# Documents


Click [Documents](https://docs.python.org/3/tutorial/errors.html)


# SyntaxError

SyntaxError are entirely on you to solve, it is a problem that you've got to go back into your code and fix.
You can't hope for it to solve itself.

### Code Example
Click [[Hello.py#Exceptions|Code Examples]]

Click [Documents](https://docs.python.org/3/tutorial/errors.html)

----

# Runtime Error
Happens while your code it running

You have to write some additional code defensively to detect when those error happens.


## ValueError

- What is ValueError ?
	- An exception that occurs when a function receives an argument of the correct data type but an inappropriate value.


### Code Example
Click [[number.py#ValueError|Code Example]]

Click [Documents](https://docs.python.org/3/tutorial/errors.html)

-----


# try, except, else, break

If you want to try to do something in Python, you can use this keyword to check whether or not something exceptional, something erroneous has happened.

Can I go and ==try== to do something ==except== if something goes wrong ?

The ==try== block lets you test a block of code for errors.
The ==except== block lets you handle the error.
The ==else== block lets you execute code when there is no errors.

##### It is better to explictly catch errors that you know might happen instead of catching everything.

## break
The ==break== keyword is used to break out a ==for== loop, or a ==while== loop.

Click [[number.py#try & except in loop|Code Example]]


## Syntax
```python
try:
	print(x)
except:
	print("An exception occurred")
else:
	print("Nothing went wrong")
```


## Best Practice
You should really only be trying to do 1 or very few lines of code that can actually raise an exception.


## Documents
Click [[number.py#Using try and except|Code Example]]
[[number.py#try & except in loop|Code Example (Looped)]]


Click [Documents](https://www.w3schools.com/python/python_try_except.asp)


-----

# NameError
- What is a NameError ?
	- Occurs when you try to use a variable, function, or module that doesn't exist or wasn't used in a valid way.

- Tend to refer to your code.


## Documents
Click [[number.py#Best Practice|Code Example]]

Click [Documents](https://www.geeksforgeeks.org/handling-nameerror-exception-in-python/)

----


# pass

- What is it used for ?
	- The pass statement is used as a placeholder for futurecode.
	- When the pass statement is executed, nothing happens, but you avoid getting an error when empty code is not allowed.
		- Empty code is not allowed in loops, functions definitions, or in if statements.

If you want to handle an exception in python but you want to pass on doing anything with it, so you want to catch it but you want to ignore it.


## Syntax
```python
for x in [0, 1, 2]:
	pass
```


## Documents
Click [[number.py#pass|Code Example]]

Click [Documents](https://www.w3schools.com/python/ref_keyword_pass.asp)

----



# raise

- What is it used for ?
	- The ==raise== keyword is used to raise an exception.

You can define what kind of error to raise, and the text to print to the user.

## Syntax
```python
x = -1

if x < 0:
	raise Exception("Sorry, no numbers below zero")
```


## Documents
Click [NOT COVERED IN LEC 3]

Click [Documents](https://www.w3schools.com/python/ref_keyword_raise.asp)
















