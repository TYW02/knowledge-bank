[[Lecture 3 - Exceptions]]

# ValueError
```python
x = int(input("What's x? "))
print(f"x is {x}")

< Input: 50
> Output: x is 50

< Input: -1
> Output: x is -1

< Input: cat
> ValueError: Invalid literal for int() with base 10: 'cat'

```
What could go wrong here ?
User can put something that is not an integer.

Error Explanation: 
	Invalid literal: Something that has been typed in.
	for int(): int() is the function you are using to convert the user's input to a int
	base 10: refers to the decimal system
Python isn't happy that we passed 'cat' to the int() function.

#### How to fix ?
- Program defensively 


## Using try and except
```python
try:
	x = int(input("What's x? "))
	print(f"x is {x}")
except ValueError:
	print("x is not an integer")

< Input: 50
> Output: x is 50

< Input: cat
> Output: x is not an integer 

```



## Best Practice
```python
try:
	x = int(input("What's x? "))
except ValueError:
	print("x is not an integer")

print(f"x is {x}")

< Input: 50
> Output: x is 50

< Input: cat
> Output: NameError: name 'x' is not defined

----------------------------------------------------------------------------------------


try:
	x = int(input("What's x? "))
except ValueError:
	print("x is not an integer")
else:
	print(f"x is {x}")

# Python will try and execute line 2
# If something goes wrong, execute line 3 and 4
# If you try and it succeeds (no error) run line 5 and 6

< Input: 50
> Output: x is 50

< Input: cat
> Output: x is not an integer
```



## try & except in loop
- Both methods work
```python
while True:
	try:
		x = int(input("What's x? "))
	except ValueError:
		print("x is not an integer")
	else:
		break
print(f"x is {x}")

< Input: 50
> Output: x is 50

< Input: cat
> Output: x is not an integer
> Output: What's x ?

----------------------------------------------------------------------------------------


while True:
	try:
		x = int(input("What's x? "))
		break
	except ValueError:
		print("x is not an integer")
		
print(f"x is {x}")

< Input: 50
> Output: x is 50

```


## Writing function
```python
def main():
	x = get_int()
	print(f"x is {x}")


def get_int():
	while True:
	try:
		x = int(input("What's x? "))
	except ValueError:
		print("x is not an integer")
	else:
		break
	return x

main()

< Input: 50
> Output: 50

< Input: cat
> Output: x is not an integer
> Output: What's x ?


----------------------------------------------------------------------------------------

def main():
	x = get_int()
	print(f"x is {x}")


def get_int():
	while True:
		try:
			x = int(input("What's x? "))
		except ValueError:
			print("x is not an integer")
		else:
			return x # return will also break you out of loop

main()

< Input: 50
> Output: 50

< Input: cat
> Output: x is not an integer
> Output: What's x ?


----------------------------------------------------------------------------------------


def main():
	x = get_int()
	print(f"x is {x}")


def get_int():
	while True:
		try:
			return int(input("What's x? "))
		except ValueError:
			print("x is not an integer")

main()



```



## pass
- You are still catching the error here, but the user isn't going to see the message.
```python

def main():
	x = get_int()
	print(f"x is {x}")


def get_int():
	while True:
		try:
			return int(input("What's x? "))
		except ValueError:
			pass

main()

< Input: cat
> Output: What's x ?
< Input: cat
> Output: What's x ?

```



## Function Arguments
```python
def main():
	x = get_int("What's x? ")
	print(f"x is {x}")


def get_int(prompt):
	while True:
		try:
			return int(input(prompt))
		except ValueError:
			pass

main()

< Input: cat
> Output: What's x ?
< Input: cat
> Output: What's x ?

```





















