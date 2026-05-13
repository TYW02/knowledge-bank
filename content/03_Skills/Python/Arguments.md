---
title: Arguments
tags:
  - Python
  - Arguments
---

# Passing an Arbitrary number of Arguments

Sometimes you don't know ahead of time how many arguments a function needs to accept.

```python
def make_pizza(*toppings):
	print(toppings)
	
make_pizza("pepperoni")
make_pizza("mushrooms", "green peppers", "extra cheese")
```

## Using Arbitrary keyword arguments
Function that accepts key-value pair

```python
def build_profile(first, last, **user_info):
	user_info['first_name'] = first
	user_info['last_name'] = last
	return user_info
	
user_profile = build_profile('albert', 'einstein',
	location = 'princeton',
	field = 'physics')
	
# [Output]:
{'location': 'princeton', 'field': 'physics',
'first_name': 'albert', 'last_name': 'einstein'}

```