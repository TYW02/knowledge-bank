Python Program: [[names.py]], [[students.py]], [[costumes.py]]
Topic Covered: 
Current Status:
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox" > |   |
> | Completed | <input type="checkbox" checked> | |  

Youtube link: [Here](https://www.youtube.com/watch?v=KD-Yoel6EVQ&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=11&t=26s)

----



# open
- What does it do ?
	- The open() function opens a file, and returns it as a file object.

## Syntax
```python
open(file, mode)
```

## Parameter Values
| Parameter | Description                   |
| --------- | ----------------------------- |
| *file*    | The path and name of the file |
| *mode*    | A string, define which mode you want to open the file in: <br /><br />"r" - Read - Default Value. Opens a file for reading, error if the file does not exist <br />"a" - Append - Opens a file for appending, creates the file if it does not exist <br /> "w" - Write - Opens a file for writing, creates the file if it does not exist <br /> "x" - Create - Creates the specified file, returns an error if the file exist <br /> <br />In addition you caqn specify if the file should be handled as binary or text mode <br /> <br />"t" - Text - Default value. Text Mode <br /> "b" - Binary - Binary Mode (e.g images)                            |


## Example
```python
f = open("demofile.txt", "r")
print(f.read())
```

## Documents
Click [[names.py#Saving in File I/O]|Code Example]]
Click [Documents](https://www.w3schools.com/python/ref_func_open.asp)

----

# with
Automatically opens and close files for you 

## Syntax
```python
with open("file.txt", "r") as file:
	file.write("write something")
```

## Documents
Click [[names.py#Automatically open and close files using with|Code Example]]
Click [Documents](https://www.geeksforgeeks.org/with-statement-in-python/)

----


# sorted

- What does it do ?
	- The sorted() function returns a sorted list of the specified iterable object.
	- You can specify ascending or descending order. Strings are sorted alphabetically, and numbers are sorted numerically.

>[!INFO]
>You cannot sort a list that contains BOTH string values AND numeric values.


## Syntax
```python
sorted(iterable, key=key, reverse=reverse)
```


## Parameter Values
| Paramter   | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| *iterable* | Required. The sequence to sort, list, dictionary, tuple etc.         |
| *key*      | Optional. A Function to execute to decide the order. Default is None |
| *reverse*  | Optional. A Boolean. False will sort ascending, True will sort descending. Default is False                                                                 |


## Example
```python
a = ("b", "g", "a", "d", "f", "c", "h", "e")
x = sorted(a)
print(x)
```


## Documents
Click [[names.py#Sorting the output in order|Code Example]]
Click [Documents](https://www.w3schools.com/python/ref_func_sorted.asp)

----



# Lambda Functions

- What is it ?
	- A lambda function is a small anonymous function.
	- A lambda function can take any number of arguments, but can only have one expression

## Syntax
```python
lambda arguments: expression
```


## Example
```python
x = lambda a: a + 10
print(x(5))
```
> [!INFO]
> Lambda functions can take any number of arguments


## Documents
Click [[students.py#Lambda Functions|Code Example]]
Click [Documents](https://www.w3schools.com/python/python_lambda.asp)


----


# csv library


## Documents
Click [[students.py#Using csv library|Code Example]]
Click [Documents](https://docs.python.org/3/library/csv.html)


----



# PIL library




## Documents
Click [[costumes.py#Creating a custom GIF|Code Example]]
Click [Documents](https://pillow.readthedocs.io/en/stable/)

----


