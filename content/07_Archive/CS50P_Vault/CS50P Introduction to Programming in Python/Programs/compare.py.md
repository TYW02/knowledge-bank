Tags: [[Lecture 1 - Conditionals]] 


## Comparing x < y and using IF
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

if x < y:
	print("x is less than y") 
if x > y:
	print("x is greater than y")
if x == y:
	print("x is equal to y")

< Input: 1
< Input: 2

> Output: x is less than y
```



## Using elif
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

if x < y:
	print("x is less than y") 
elif x > y:
	print("x is greater than y")
elif x == y:
	print("x is equal to y")

< Input: 1
< Input: 2

> Output: x is less than y
```



## Using else
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

if x < y:
	print("x is less than y") 
elif x > y:
	print("x is greater than y")
else:
	print("x is equal to y")

< Input: 1
< Input: 2

> Output: x is less than y
```


## Using or
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

if x < y or x > y:
	print("x is not equal to y")
else:
	print("x is equal to y")

< Input: 1
< Input: 2

> Output: x is not equal to y

< Input: 1
< Input: 1

> Output: x is equal to y
```



## Using != not equal
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

if x != y:
	print("x is not equal to y")
else:
	print("x is equal to y")
	
< Input: 1
< Input: 2

> Output: x is not equal to y
```


## Using == equal
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

if x == y:
	print("x is equal to y")
else:
	print("x is not equal to y")
	
< Input: 1
< Input: 1

> Output: x is equal to y
```



























