---
title: Classes
tags:
  - Classes
---
# Defining a Class
```python
class Dog:
	def __init__(self, name, age):
		self.name = name
		self.age = age
		
	def sit(self):
		print(f"{self.name} is now sitting")
		
	def roll_over(self):
		print(f"{self.name} rolled over!")
```

## The init method

The init method is a special method that Python runs automatically whenever we create a new instance based on the Dog class.

Any variable prefixed with *self* is available to every method in the class, and we'll also be able to access these variables through any instance created from the class. 