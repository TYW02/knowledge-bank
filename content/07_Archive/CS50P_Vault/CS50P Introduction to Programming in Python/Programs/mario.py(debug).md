Tags: [[Debugging]]



## Using print() to debug
```python
def main():
	height = int(input("Height: "))
	pyramid(height)

def pyramid(n):
	for i in range n:
		print("#" * i)

if __name__ == "__main__":
	main()

< Input: 3
> Output: 
#
##

----------------------------------------------------------------------------------------

def main():
	height = int(input("Height: "))
	pyramid(height)

def pyramid(n):
	for i in range n:
		print(i, end=" ")
		print("#" * i)

if __name__ == "__main__":
	main()

< Input: 3
> Output: 
0
1 #
2 ##

----------------------------------------------------------------------------------------

def main():
	height = int(input("Height: "))
	pyramid(height)

def pyramid(n):
	for i in range n:
		print("#" * (i + 1))

if __name__ == "__main__":
	main()

< Input: 3
> Output: 
#
##
###

```



## Using built-in debugger (breakpoint)
```python
def main():
	height = int(input("Height: "))
	pyramid(height)

def pyramid(n):
	for i in range n:
		print("#" * i)

if __name__ == "__main__":
	main() # Set breakpoint here

< Input: 3
> Output: 
#
##
```






