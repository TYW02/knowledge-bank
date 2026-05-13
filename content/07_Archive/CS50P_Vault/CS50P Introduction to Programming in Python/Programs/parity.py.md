Tags: [[Lecture 1 - Conditionals]] [[Lecture 0 - Functions, Variables]]



## Modulo
```python
x = int(input("What's x? "))

if x % 2 == 0:
	print("Even")

else:
	print("Odd")

< Input: 2
> Output: Even

< Input: 3
> Output: Odd
```


## Writing a function
```python
def main():
	x = int(input("What's x? "))

	if is_even(x):
		print("Even")
	else:
		print("Odd")

def is_even(n)
	if n % 2 == 0:
		return True
	else:
		return False

main()

< Input: 2
> Output: Even

< Input: 3
> Output: Odd
```


## Pythonic Expression
```python
def main():
	x = int(input("What's x? "))

	if is_even(x):
		print("Even")
	else:
		print("Odd")

def is_even(n):
	return (n % 2 == 0)

main()

< Input: 2
> Output: Even

< Input: 3
> Output: Odd
```
