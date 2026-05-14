---
title: Storing Data
tags:
  - JSON
---
```python
import json
numbers = [2, 3, 5, 7, 11, 13]
path = Path('numbers.json')
contents = json.dumps(numbers)
path.write_text(contents)
```

`json.dumps()` takes data to be converted to json and returns a string that is to be written to a file.

## Saving & Reading User-generated Data
```python
path = Path('username.json')
if path.exists():
	contents = path.read_text()
	username = json.loads(content)
	print(f"Welcome back, {username}!")
else:
	username = input("What is your name?")
	contents = json.dumps(username)
	path.write_text(contents)
	print(f"We'll remember you when you come back, {username}!")
```

