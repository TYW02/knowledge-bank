Tags: [[Lecture 5 - Unit Tests]]

## Import hello.py
```python
def main():
	name = input("What's your name? ")
	print(hello(name))

def hello(to="world"):
	return f"hello, {to}"

main()

```




## Unit test hello
```python
from hello import hello

def test_hello():
	assert hello("David") == "hello, David"
	assert hello() == "hello, world"

$ pytest test_hello.py
.
1 passed in 0.00s

```


## Improving the design
```python
from hello import hello

def test_default():
	assert hello() == "hello, world"

def test_argument():
	assert hello("David") == "hello, David"

$ pytest test_hello.py
..
2 passed in 0.01s
```


## Asserting in loops
```python
from hello import hello

def test_default():
	assert hello() == "hello, world"

def test_argument():
	for name in ["Hermione", "Harry", "Ron"]
	assert hello(name) == f"hello, {name}"
```
- Although you can test in a loop you should keep your test small and simple.
- Because you don't want to write too long of a code to where your test is flawed.



