Tags: [[Lecture 0 - Functions, Variables]],[[Lecture 3 - Exceptions]], [[Lecture 5 - Unit Tests]]



## Starting out
```python
input("What's your name ? ")
print("hello, world")
```




## Using Variables and Return Values
```python
name = input("What's your name ?")
print("hello, ")
print(name)
```



## Adding Comments
```python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
print("hello, ")
print(name)
```



## Pseudocode
```python
# Ask user for their name

# Say hello to user
```




## Improvements
```Python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
print("hello, " + name)
```



## Multi argument print
```python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
# When you pass multiple arguments to print it auto spaces for you
print("hello,", name)
```


## Overriding print(end='\\n')
```python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
print("hello,", ends="")
print(name)

> Output: hello, David
 
print("hello,", ends="???")
print(name)

> Output: hello, ???David

```


## Overriding print(sep" ")
```python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
print("hello,",name, sep"???")

> Output: hello,???David
```



## Printing quotes
```python
# Using different quotes
print('hello, "friend"')

> Output: hello, "friend"

# Escape quote version
print("hello, \"friend\"")

> Output: hello, "friend"

```



## Using {} format string / f-string

^6f074c

```python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
print(f"hello, {name}")

> Output: hello, David
```


## User giving wrong input (Whitespace)
```python
# Ask user for their name
name = input("What's your name ?")

# Say hello to user
print(f"hello, {name}")

< Input:         david      
> Output: hello,          david

```

### How to fix wrong user input (Whitespace)

^4b0f17

```python
# Ask user for their name
name = input("What's your name ?")

# Remove whitespace from str
name = name.strip()

# Say hello to user
print(f"hello, {name}")

< Input:         david 
> Output: hello, david
```


## Capitalize User input

^0298c8

```python
# Ask user for their name
name = input("What's your name ?")

# Capitalize user's name
name = name.capitalize()

# Say hello to user
print(f"hello, {name}")

< Input:         david 
> Output: hello, David


< Input:         david malan
> Output: hello, David malan

```


## Using .title() for User input
```python
# Ask user for their name
name = input("What's your name ?")

# Remove whitespace from str
name = name.strip()

# Capitalize user's name
name = name.title()

# Say hello to user
print(f"hello, {name}")

< Input:          david malen
> Output: hello, David Malen
```


## Chaining Functions together
```python
# Ask user for their name
name = input("What's your name ?")

# Remove whitespace from str and capitalize user's name
name = name.strip().title()

# Say hello to user
print(f"hello, {name}")

< Input:          david malen
> Output: hello, David Malen
```


## Best Practice
```python
# Ask user for their name
name = input("What's your name ?").strip().title()

# Say hello to user
print(f"hello, {name}")

< Input:          david malen
> Output: hello, David Malen

----------------------------------------------------------------------------------------

# Ask user for their name
name = input("What's your name ?")
name = name.strip()
name = name.title()

# Say hello to user
print(f"hello, {name}")

< Input:          david malen
> Output: hello, David Malen

```



## .split()
```python
# Ask user for their name
name = input("What's your name ?").strip().title()

# Split user's name into first name and last name
first, last = name.split(" ")

# Say hello to user
print(f"hello, {first}")

< Input:david malen
> Output: hello, David
```




## Creating function
```python
def hello(to):
	print("hello,", to)


name = input("What's your name? ")
hello(name)

< Input: David
> Output: hello, David

```


## Setting default value in function
```python
def hello(to="world"):
	print("hello,", to)


hello()
name = input("What's your name? ")
hello(name)


> Output: hello, world
< Input: David
> Output: hello, David
```


## Placement of function
```python
def main():
	name = input("What's your name? ")
	hello(name)

def hello(to="world"):
	print("hello,", to)

main()

```


## Exceptions Syntax
```python
print("hello, world)

> SyntaxError: unterminated string literal (detected at line 1)
```
unterminated --> would generally mean that you started something but didn't stop it.
string --> is a sequence of text.
literal --> refers to something you typed.

Fix --> terminate the string that you typed.



