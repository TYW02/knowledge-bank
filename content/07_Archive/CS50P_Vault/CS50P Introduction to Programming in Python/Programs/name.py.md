Tags: [[Lecture 4 - Libraries]]



## Sys
```python
import sys

print("hello, my name is", sys.argv[1])

CLI:
$ python name.py David

> Output: hello, my name is David

$ python name.py

> IndexError: list index out of range 
----------------------------------------------------------------------------------------

import sys

print("hello, my name is", sys.argv[0])

CLI:
$ python name.py 

> Output: hello, my name is name.py

```

- You use sys.argv[1] here because sys.argv[0] will return you the name of the program.


## Improving Sys
```python
import sys

try:
	print("hello, my name is", sys.argv[1])
except IndexError:
	print("Too few arguments")

$ python name.py 

> Output: Too few arguments

$ python name.py David

> Output: hello, my name is David

```




## Defensive version
```python
import sys

if len(sys.argv) < 2:
	print("Too few arguments")
elif len(sys.argv) > 2:
	print("Too many arguments")
else:
	print("hello, my name is", sys.argv[1])

$ python name.py 
> Output: Too few arguments

$ python name.py David Malen
> Output: Too many arguments

$ python name.py David
> Output: hello, my name is David


```




## Making it look nice
```python
import sys

# Check for errors
if len(sys.argv) < 2:
	sys.exit("Too few arguments")
elif len(sys.argv) > 2:
	sys.exit("Too many arguments")

# Print name tags
print("hello, my name is", sys.argv[1])

$ python name.py 
> Output: Too few arguments

$ python name.py David Malen
> Output: Too many argument

$ python name.py David
> Output: hello, my name is David
```
- What sys.exit does is that it stops the program right there.
	- We do that here because if you gave too few arguments there is nothing we can do other than exit the program.



## Supporting multiple command line input
```python
import sys

# Check for errors
if len(sys.argv) < 2:
	sys.exit("Too few arguments")


for arg in sys.argv:
	print("hello, my name is", arg)

$ python name.py David Carter Rongxin
> hello, my name is name.py
> hello, my name is David
> hello, my name is Carter
> hello, my name is Rongxin  

----------------------------------------------------------------------------------------

import sys

# Check for errors
if len(sys.argv) < 2:
	sys.exit("Too few arguments")


for arg in sys.argv[1:]:
	print("hello, my name is", arg)

$ python name.py David Carter Rongxin
> hello, my name is David
> hello, my name is Carter
> hello, my name is Rongxin  

----------------------------------------------------------------------------------------

import sys

# Check for errors
if len(sys.argv) < 2:
	sys.exit("Too few arguments")


for arg in sys.argv[1:-1]:
	print("hello, my name is", arg)

$ python name.py David Carter Rongxin
> hello, my name is David
> hello, my name is Carter

```











