Tags: [[Lecture 4 - Libraries]]


# Custom Library
```python
def main():
	hello("world")
	goodbye("world")


def hello(name):
	print(f"hello, {name}")

def goodbye(name):
	print(f"goodbye, {name}")

main()

> Output:
> hello, world
> goodbye, world

```



# run main() only in lib file
```python
def main():
	hello("world")
	goodbye("world")


def hello(name):
	print(f"hello, {name}")

def goodbye(name):
	print(f"goodbye, {name}")

if __name__ = "__main__":
	main()


```