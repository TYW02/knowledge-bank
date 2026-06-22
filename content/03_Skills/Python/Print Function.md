---
title: Print Function
tags:
  - Print
---
# Syntax
```python
print(object(s), sep=separator, end=end, file=file, flush=flush)
```

| Parameter       | Description                                                                                           |
| --------------- | ----------------------------------------------------------------------------------------------------- |
| object(s)       | Any object, and as many as you like. Will be converted to string before printed                       |
| sep='separator' | Optional. Specify how to separate the objects, if there is more than one. Default is ' '              |
| end='end'       | Optional. Specify what to print at the end. Default is '\n'                                           |
| file            | Optional. An object with a write method. Default is sys.stdout                                        |
| flush           | Optional. A boolean, specifying if the output is flushed (True) or buffered (False). Default is False |

## Object
```python
print('Bob')
print('Bob', True, 25)
# Output
Bob
Bob True 25
```

## Separator
```python
people: list[Any] = ['Bob', 'James', 'Sandra']
print(*people, sep=', ')
print(*people, sep='-')

# Output
Bob, James, Sandra
Bob-James-Sandra
```

## End
```python
people: list[Any] = ['Bob', 'James', 'Sandra']
print(*people, sep=', ', end='.\n')
print(*people, sep='-', end='!\n')

# Output
Bob, James, Sandra.
Bob-James-Sandra!
```

> [!NOTE]
> For this you have to remember to have the `\n` at the end else everything will be printed in 1 line.


## File
```python
from random import randint
from typing import TextIO

log_file: TextIO = open('app.log', 'a')
print(f'Roll: {randint(1, 10)}', file=log_file)

# Output
The print statement will be printed into the app.log file
```


## Flush
```python
import time

for i in range(5):
	print(f'{i}', end='', flush=True)
	time.sleep(1)
```

> [!NOTE]
> Here, the print statement will print 0 then wait a second print 1 wait print 2 wait print 3 ...
> If it was set to False, you won't see anything happen for 5 seconds before 0 - 4 is printed.
> Use this, if you want to see updates immediately.

