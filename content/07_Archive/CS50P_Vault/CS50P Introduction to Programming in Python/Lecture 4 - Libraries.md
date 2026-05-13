Python Program: [[sayings.py]], [[say.py]], [[itunes.py]], [[name.py]], [[average.py]], [[generate.py]]
Topic Covered: #Modules, #Library, #Slice, #APIs
Current Status:
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox" > |   |
> | Completed | <input type="checkbox" checked> | |  

Youtube link: [Here](https://www.youtube.com/watch?v=MztLZWibctI&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=8&t=1s)

----



# Modules

- What is a module ?
	- A module is a file containing a set of functions you want to include in your application.

## Creating a Module
```python
def greeting(name):
	print("Hello, " + name)
```
> [!INFO]
> Save this code in a file named mymodule.py


## Using a Module
- Now we can use the module we just created, by using the ==import== statement:
```python
import mymodule

mymodule.greeting("Jonathan")
```
> [!INFO]
> Import the module named mymodule, and call the greeting function
> 
> Note: When using a function from a module, use the syntax: *module_name.function_name*


## Variables in Module
- The module can contain functions, as already described, but also variables of all types (arrays, dictionaries, objects etc):

```python
person1 = {
	"name": "John",
	"age": 36,
	"country": "Norway"
}
```
>[!INFO]
>Save this code in the file mymodule.py


```python
import mymodule

a = mymodule.person1["age"]
print(a)
```
> [!INFO]
> Import the module named mymodule, and access the person1 dictionary



## Documents
Click

Click [Documents](https://www.w3schools.com/python/python_modules.asp)


----




# random

- Python has a built-in module that you can use to make random numbers.


## random.randint(a, b)

- What is it used for ?
	- The *randint()* method returns an integer number selected element from the specified range.

### Syntax
```python
import random

print(random.randint(3, 9))
# Gives you from 3 to 9
----------------------------------------------------------------------------------------

random.randint(start, stop)
```

#### Parameter Values
| Parameter | Description                                                 |
| --------- | ----------------------------------------------------------- |
| *start*   | Required. An integer specifying at which position to start. |
| *stop*    | Required. An integer specifying at which position to end.                                                            |

-----


## random.shuffle(x)
- What does it do ?
	- The *shuffle()* method takes a sequence, like a list, and reorganize the order of the items.
> [!INFO]
> **Note**: This method changes the original list, it does not return a new list


## Syntax
```python
random.shuffle(sequence)
```

## Parameter Values
| Parameter  | Description          |
| ---------- | -------------------- |
| *sequence* | Required. A Sequence |
| *function* | ==Deprecated since Python 3.9. Removed in Python 3.11== Optional. The name of a function that returns a number between 0.0 and 1.0. If not specified, the function ==random()== will be used.                     |



## Documents
Click [[generate.py#Using random.choice|Code Example]], [[generate.py#randint()|Code Example (2)]], [[generate.py#]]

Click [Documents](https://www.w3schools.com/python/module_random.asp)


-----



# from

- What is it used for ?
	- The ==from== keyword is used to import only a specified section from a module.


## Syntax
```python
from datetime import time

x = time(hour=15)

print(x)
```
> [!INFO]
> Import only the *time* section from the datetime module, and print the time as if it was 15:00


## Documents
Click 

Click [Documents](https://www.w3schools.com/python/ref_keyword_from.asp)


## Related Pages
The [[#Using a Module|import]] keyword.



----


# statistics
- Python has a built-in module that you can use to calculate mathematical statistics of numeric data.

## Documents
Click [[average.py#Statistics|Code Example]]

Click [Documents](https://www.w3schools.com/python/module_statistics.asp)


-----



# Command-line arguments

## Sys
- Provides functions and variables used to manipulate different parts of the Pythong runtime environment.
	- Main Purpose:
		1. List of command line arguments
		2. len(sys.argv) provides the number of command line arguments


## Documents
Click [[name.py#Sys|Code Example: Sys.argv]]
Click [[name.py#Making it look nice|Code Example: Sys.exit]]

Click [Document For Command-line Argument](https://www.geeksforgeeks.org/command-line-arguments-in-python/)
Click [Document For Sys](https://docs.python.org/3/library/sys.html)



----



# slices
- What is it used for ?
	- You can return a range of characters by using the slice syntax.
	- Specify the start index and the end index, separated by a colon, to return a part of the string.


## Syntax
```python
b = "Hello, World!"
print(b[2:5])

> Output: llo
```
> [!INFO]
Gets Characters from position 2 to 5(not included 
NOTE: The first character has index 0.



## Documents
Click [[name.py#Supporting multiple command line input|Code Example]]

Click [Documents](https://www.w3schools.com/python/python_strings_slicing.asp)


----



# packages

- What is a package
	- A third party library that you can install on your PC 



## Find packages here
Click [Link](https://pypi.org/)


----




# APIs
- You can use the *requests* package which allows you to make web requests, using python code.

If it is written in code, you are basically pretending to be the browser then taking the reply from the server and using it in your code.

## Documents
Click [Package Link](https://pypi.org/project/requests/)


----




# Custom Library


# Documents
Click [[sayings.py#Custom Library|Code Examples]]


## \_\_name__
- Since there is no main() function in Python, when the command to run a python program is given to the interpreter, the code that is at level 0 indentation is to be executed.

##### If the source file is executed as the main program, the interpreter sets the \_\_name\_\_ variable to have a value of "__main__"

##### If this file is being imported from another module, \_\_name\_\_ will be set to the module's name.


## Documents
Click [[sayings.py#run main() only in lib file|Read]], [[say.py#Custom library|Both]]

Click [Documents](https://www.geeksforgeeks.org/__name__-a-special-variable-in-python/)


----

















































