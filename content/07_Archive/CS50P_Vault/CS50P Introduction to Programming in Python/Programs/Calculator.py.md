Tags: [[Lecture 0 - Functions, Variables]], [[Lecture 5 - Unit Tests]]

# Initial Code
```python
x = input("What's x? ")
y = input("What's y? ")

z = x + y

print(z)

< Input: 1
< Input: 2

> Output: 12
```

This isn't working because we are concatenating 2 text together.
Because the user is always typing on their phone, keyboard the input is always as **text**


## Converting String to integer

```python
x = input("What's x? ")
y = input("What's y? ")

z = int(x) + int(y)

print(z)

< Input: 1
< Input: 2

> Output: 3
```


## Cutting down code
```python
x = int(input("What's x? "))
y = int(input("What's y? "))

print(x + y)

< Input: 1
< Input: 2

> Output: 3
```


## Float() input
```python
x = float(input("What's x? "))
y = float(input("What's y? "))

print(x + y)

< Input: 1.2
< Input: 3.4

> Output: 4.6
```


## round()
```python
x = float(input("What's x? "))
y = float(input("What's y? "))

z = round(x + y)

print(z)

< Input: 1.2
< Input: 3.4

> Output: 5
```



## f-string (Adding , every 000)
```python
x = float(input("What's x? "))
y = float(input("What's y? "))

z = round(x + y)

print(f"{z:,}")

< Input: 999
< Input: 1

> Output: 1,000

```


## Division
```python

x = float(input("What's x? "))
y = float(input("What's y? "))

z = x / y

print(z)

< Input: 2
< Input: 3

> Output: 0.66666666

```


## Rounding with Division
```python
x = float(input("What's x? "))
y = float(input("What's y? "))

z = round(x / y, 2)

print(z)

< Input: 2
< Input: 3

> Output: 0.67
```

## f-string with division
```python 
x = float(input("What's x? "))
y = float(input("What's y? "))

z = x / y

print(f"{z:.2f}")

< Input: 2
< Input: 3

> Output: 0.67
```


## Using Return
```python
def main():
	x = int(input("What's x? "))
	print("x squared is", square(x))


def square(n):
	return n * n

main()

< Input: 2
> Output: x squared is 4

```



## Start of Unit test
```python
def main():
	x = int(input("What's x? "))
	print("x squared is", square(x))


def square(n):
	return n * n

if __name__ == "__main__"
	main()
```













