#Functions 
https://www.geeksforgeeks.org/python/python-programming-language-tutorial/
https://www.geeksforgeeks.org/python/python-functions/
## What is a function ?
**Functions** is a block of statements that does a specific task.
- The idea is to put commonly/repeatedly done task together and make a function so that instead of writing the same code, we can do the function call to reuse code.

## Benefit of using functions
- Code Reuse
- Reduced code length
- Increased readability of code


# Python Function Declaration
The syntax to declare a functions is:
![[51.png]]

##  Types of Functions in Python
- **Built-in library function**: These are Standard functions in Python that are available to use.
- **User-defined function**: We can create our own functions based on our requirements.


## What is def ?
The **def keyword** stands for Define. It is used to create a **user-defined function**.
It marks the beginning of a function block and allows you to group a set of statements so they can be reused when the function is called.
### Syntax:
```python
def function_name(parameters):
	# function body
```
### Explanation:
- **def**: Starts the function definition
- **function_name**: Name of the function
- **parameters**: Inputs passed to the function (inside ()), optional.
- **:**  Indicates the start of the function body
- **Indented code**: The function body that runs when called.

## Calling a Function in Python
After creating a function in Python we can call it by using the name of the functions followed by the parenthesis containing parameters of that particular function
```python
def fun():
	print("Welcome to GFG")
	
# Driver code to call a function
fun()

# Welcome to GFG
```


# Python Function Arguments
Arguments are the values passed inside the parenthesis of the function. A function can have any number of arguments separated by a comma.

### Syntax for functions with arguments:
```python
def function_name(parameter: data_type) -> return_type:
	"""Docstring"""
	# body of the function
	return expression
```

**data_type** and **return_type** are optional in function declaration, meaning the same function can also be written as:
```python
def function_name(parameter):
	"""Docstring"""
	# body of the function
	return expression
```

### Example:
```python
def evenOdd(x: int) -> str:
	if (x % 2 == 0):
		return "Even"
	else:
		return "Odd"
		
print(evenOdd(16))
print(evenOdd(7))

# Even
# Odd
```

### Example (Without Typehints):
```python
def evenOdd(x):
	if (x % 2 == 0):
		return "Even"
	else:
		return "Odd"
		
print(evenOdd(16))
print(evenOdd(7))

# Even
# Odd
```


# Types of Python Function Arguments

- [[Functions#Default Arguments|Functions]] 
- [[Functions#Keyword Arguments|Keyword Arguments (named arguments)]]
- [[Functions#Positional Arguments|Positional Arguments]]
- [[Functions#Arbitrary Keyword Arguments|Arbitrary Arguments (variable-length arguments `*args` and `**kwargs`)]]

### Default Arguments
#DefaultArguments
A default argument is a parameter that assumes a default value if a value is not provided in the function call for that argument
```python
def myFun(x, y=50):
	print("x: ", x)
	print("y: ", y)
	
myFun(10)

# x: 10
# y: 50
```


### Keyword Arguments
#KeywordArguments
The idea is to allow the caller to specify the argument name with values so that the caller does not need to remember the order of parameters
```python
def student(fname, lname):
	print(fname, lname)
	
student(fname="Geeks", lname="Practice")
student(lname="Practice", fname="Geeks")

# Geeks Practice
# Geeks Practice
```


### Positional Arguments
#PostionalArguments
We use positional arguments so that the first argument (or value) is assigned to name and the second argument is assigned to age.
- By changing the position, or if you forget the order of the position, the values can be used in the wrong places, as shown
```python
def nameAge(name, age):
	print("Hi, I am", name)
	print("My age is ", age)
	
print("Case 1:")
nameAge("Suraj", 27)

print("Case 2:")
nameAge(27, "Suraj")

# Case-1:
# Hi, I am Suraj
# My age is  27

# Case-2:
# Hi, I am 27
# My age is  Suraj
```


### Arbitrary Keyword Arguments
#ArbitraryKeyword
In Python Arbitrary Keyword Arguments, [`*args`, and `**kwargs`](https://www.geeksforgeeks.org/python/args-kwargs-python/) can pass a variable number of arguments to a function using special symbols. There are two special symbols:

- `*args` in Python (Non-Keyword Arguments)
- `**kwargs` in Python (Keyword Arguments)

Example 1: Variable length non-keywords arguments
```python
def myFun(*argv):
    for arg in argv:
        print(arg)


myFun('Hello', 'Welcome', 'to', 'GeeksforGeeks')

# Hello
# Welcome
# to
# GeeksforGeeks
```

Example 2: Variable length keyword arguments
```python
def myFun(**kwargs):
    for key, value in kwargs.items():
        print("%s == %s" % (key, value))


myFun(first='Geeks', mid='for', last='Geeks')

# first == Geeks
# mid == for
# last == Geeks
```


# Python Function within Functions
A function that is defined inside another function is known as the **inner function** or **nested function**. Nested functions can access variables of the enclosing scope. Inner functions are used so that they can be protected from everything happening outside the function.

```python
def f1():
    s = 'I love GeeksforGeeks'
    
    def f2():
        print(s)
        
    f2()

f1()

# I love GeeksforGeeks
```


# Anonymous Functions in Python
#lambda
In Python, an [anonymous function](https://www.geeksforgeeks.org/python/python-lambda-anonymous-functions-filter-map-reduce/) means that a function is without a name. As we already know the def keyword is used to define the normal functions and the lambda keyword is used to create anonymous functions.

```python
def cube(x): return x*x*x   # without lambda

cube_l = lambda x : x*x*x  # with lambda

print(cube(7))
print(cube_l(7))

# 343
# 343
```


## Pass by Reference and Pass by Value
One important thing to note is, in Python every variable name is a reference. When we pass a variable to a function Python, a new reference to the object is created. Parameter passing in Python is the same as reference passing in Java.
```python
# Here x is a new reference to same list lst
def myFun(x):
    x[0] = 20

# Driver Code (Note that lst is modified
# after function call.
lst = [10, 11, 12, 13, 14, 15]
myFun(lst)
print(lst)

# [20, 11, 12, 13, 14, 15]
```

When we pass a reference and change the received reference to something else, the connection between the passed and received parameters is broken. For example, consider the below program as follows:
```python
def myFun(x):
    x = [20, 30, 40]


lst = [10, 11, 12, 13, 14, 15]
myFun(lst)
print(lst)

# [10, 11, 12, 13, 14, 15]
```


# Recursive Functions in Python
**Recursion** in Python refers to when a function calls itself. There are many instances when you have to build a recursive function to solve **Mathematical and Recursive Problems.**

Using a recursive function should be done with caution, as a recursive function can become like a non-terminating loop. It is better to check your exit statement while creating a recursive function.
```python
def factorial(n):
    if n == 0:  
        return 1
    else:
        return n * factorial(n - 1) 
      
print(factorial(4))

# 24
```


# Why Python Uses 'Self' as Default Argument

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand  # Set instance attribute
        self.model = model  # Set instance attribute

    def display(self):
        return self.brand, self.model

# Create an instance of Car
car1 = Car("Toyota", "Corolla")

# Call the display_info method
print(car1.display())  # Output: This car is a Toyota Corolla

# ('Toyota', 'Corolla')
```

### Explanation:
- self in `__init__` : Used to assign values (brand and model) to the specific instance (car1)
- self in display_info: Refers to the same car1 instance to access its attributes (brand and model)
- Python automatically passes car1 as the first argument to display

## Why is 'Self' the default argument
The main reason Python uses self as the default argument is to make [object-oriented programming](https://www.geeksforgeeks.org/dsa/introduction-of-object-oriented-programming/) explicit rather than implicit. 
By requiring the instance of the class to be passed explicitly as the first parameter to every instance method, Python ensures that the code is clear and unambiguous. This explicit approach makes it immediately obvious that methods are operating on an instance of the class, which enhances code readability and avoids confusion, especially in complex inheritance scenarios.

## Why not Implicit ?
Unlike some other programming languages, Python requires self explicitly because:

- *Clarity:* Explicit is better than implicit (Python’s philosophy).
- **Flexibility**: You can name it anything, but self is a convention.
- **Consistency**: All instance methods in Python use this approach, making it uniform.


### Example 1: Object Initialization & Method Invocation
```python
class gfg:
    def __init__(self, topic):
        self._topic = topic  # Rename the instance variable to avoid conflict

    def topic(self):
        print("Topic:", self._topic)  # Access the renamed variable

# Creating an instance of gfg
ins = gfg("Python")

# Calling the topic method
ins.topic()

# Topic: Python
```

*Explanation:* In this example, 'self' is used to refer to the instance of the class, 'ins.' Without the explicit use of 'self,' it would be unclear which instance the method is referring to and the code might become ambiguous.

# Python Lambda Function
#lambda 

**Python Lambda Functions** are anonymous functions means that the function is without a name. As we already know the __def__ keyword is used to define a normal function in Python. Similarly, the __lambda__ keyword is used to define an anonymous function in [Python](https://www.geeksforgeeks.org/python/python-programming-language-tutorial/). 

In the example, we defined a lambda function(**upper**) to convert a string to its upper case using [upper()](https://www.geeksforgeeks.org/python/python-string-upper/).
```python
s1 = 'GeeksforGeeks'

s2 = lambda func: func.upper()
print(s2(s1))

# GEEKSFORGEEKS
```

### Python Lambda Function Syntax
```python
Syntax: lambda arguments: expression
```
- lambda: The keyword to define the function
- arguments: A comma-separated list of input parameters (like in a regular function)
- expressions: A single expression that is evaluated and returned

## Lambda with Condition Checking
```python
# Example: Check if a number is positive, negative, or zero
n = lambda x: "Positive" if x > 0 else "Negative" if x < 0 else "Zero"

print(n(5))   
print(n(-3))  
print(n(0))

# Positive
# Negative
# Zero
```

## Difference Between lambda and def keyword
lambda is concise but less powerful than def when handling complex logic. Let's take a look at short comparison between the two:

| Feature           | `lambda` Function                    | Regular Function (`def`)               |
| ----------------- | ------------------------------------ | -------------------------------------- |
| **Definition**    | Single expression with `lambda`.     | Multiple lines of code.                |
| **Name**          | Anonymous (or named if assigned).    | Must have a name.                      |
| **Statements**    | Single expression only.              | Can include multiple statements.       |
| **Documentation** | Cannot have a docstring.             | Can include docstrings.                |
| **Reusability**   | Best for short, temporary functions. | Better for reusable and complex logic. |
```python
# Using lambda
sq = lambda x: x ** 2
print(sq(3))

# Using def
def sqdef(x):
    return x ** 2
print(sqdef(3))
```


### Lambda with if-else
```python
# Example: Check if a number is even or odd
check = lambda x: "Even" if x % 2 == 0 else "Odd"

print(check(4))  
print(check(7))

# Even
# Odd
```








