---
title: Exceptions
tags:
  - Exceptions
---
# What is an Exception ?
Exception is an error that arise during a program's execution

```python
try:
	print(5/0)
except ZeroDivisionError:
	print("You can't divide by zero!")
```

## Using exception to prevent crashes
```python
while True:
	if second_number == 'q':
		break
	try:
		answer = int(first_number) / int(second_number)
	except ZeroDivisionError:
		print("You can't divide by 0!")
	else:
		print(answer)
```