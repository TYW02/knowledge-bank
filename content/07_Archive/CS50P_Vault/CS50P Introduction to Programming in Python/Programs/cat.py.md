Tags: [[Lecture 2 - Loops]]

```python
print("meow")
print("meow")
print("meow")

> Output: meow
> meow
> meow
```




## Using while Loops
```python
i = 3
while i != 3:
	print("meow")
	i = i - 1

> Output: meow
> meow
> meow

----------------------------------------------------------------------------------------

i = 0
while i < 3:
	print("meow")
	i = i + 1

> Output: meow
> meow
> meow

----------------------------------------------------------------------------------------


i = 0
while i < 3:
	print("meow")
	i += 1

> Output: meow
> meow
> meow

```

You can also do increment
It is also good habit to start the i value from 0


## Using for loop
```python
for i in [0, 1, 2]:
	print("meow")

> Output: meow
> meow
> meow

----------------------------------------------------------------------------------------


for i in range(3):
	print("meow")

> Output: meow
> meow
> meow

```


## Pythonic Expression
```python
for _ in range(3):
	print("meow")


> Output: meow
> meow
> meow
 
----------------------------------------------------------------------------------------

print("meow" *3)

> Output: meowmeowmeow

----------------------------------------------------------------------------------------

print("meow\n" *3, end"")

> Output:
> meow 
> meow 
> meow


```


## Getting user input that matches a certain value 
```python
while True:
	n = int(input("What's n?"))
	if n > 0:
		break

for _ in range(n):
	print("meow")

| System: What's n ?
< Input: 5
> Output:
> meow
> meow
> meow
> meow
> meow

```


## Defining function
```python
def main():
	number = get_number()
	meow(number)

def get_number():
	while True:
		n = int(input("What's n?"))
		if n > 0:
			return n

def meow(n):
	for _ in range(n):
		print("meow")

main()

| System: What's n ?
< Input: 3
> Output: meow
> meow
> meow

```