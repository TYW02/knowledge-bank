---
title: Good Function Habits
tags:
  - Functions
---
# Specify return type for functions
```python
def read(var):
	print(f'{var=}')
	return 1
	
combined: str = read('Apple') + 'Text'
print(combined) # This would result in an error

def read(var) -> str:
	print(f'{var=}')
	return str(var)
```


# Specify parameter type
```python
def combine_as_int(a, b) -> int:
	return int(a + b)
	
print(combine_as_int('A', 'B')) # Here you get a value error

def combine_as_int(a: float, b: float) -> int:
	return int(a + b) # Here the type checker will show you a warning
```


# Avoid mutable defaults
```python
l1: list[int] = [1, 2, 3, 4, 5]

def append(number: int, target: list[int] = []) -> list[int]:
	target.append(number)
	return target
	
l2: list[int] = append(10)
l3: list[int] = append(20)

append(11, l2)
append(22, l3)
# Both l2 and l3 will return the same list

def append(number: int, target: list[int] | None = None) -> list[int]:
	if target is None:
		target = []
	target.append(number)
	return target
```


# Make function reusable
```python
MULTIPLE: int = 10

def multiply_by_ten(n: int) -> int:
	return n * MULTIPLE
	
print(multiply_by_ten(2))
# If this was moved to another file you would need another MULTIPLE

```


# Guard Clauses
```python
def strong_password(password: str) -> bool:
	has_ten_characters: bool = True
	has_uppercase: bool = True
	has_symbols: bool = True
	
	if has_ten_characters:
		if has_uppercase:
			if has_symbols:
				print('Your password is strong!')
				return True
			else:
				print('Missing symbols...')
				return False
		else:
			print('Missing uppercase...')
			return False
	else:
		print('Missing characters...')
		return False
```

### Better way to do it
```python
def strong_password(password: str) -> bool:
	has_ten_characters: bool = True
	has_uppercase: bool = True
	has_symbols: bool = True
	
	if not has_ten_characters:
		print('Missing characters...')
		return False
		
	if not has_uppercase:
		print('Missing uppercase...')
		return False
		
	if not has_symbols:
		print('Missing symbols...')
		return False
		
	print('Your password is strong!')
	return True
```













