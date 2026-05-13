Tags: [[Lecture 2 - Loops]]

# Starting
```python
print("#")
print("#")
print("#")

> Output:
> #
> #
> #
```



# For Loop
```python
for _ in range(3):
	print("#")

> Output:
> #
> #
> #
```



# Using function
```python
def main():
	print_column(3)

def print_column(height):
	for _ in range(height):
		print("#")

main()

> Output:
> #
> #
> #
```


# Printing [?]
```python
def main():
	print_row(4)

def print_row(width):
	print("?" * width)
main()

> Output:
> ????
```


# Printing squares
```python
def main():
	print_squares(3)

def print_squares(size):
	# For each brick in square
	for i in range(size):
		# For each brick in row
		for j in range(size):
			# Print brick
			print("#", end="")
	print()
main()

> Output:
> ###
> ###
> ###

```



