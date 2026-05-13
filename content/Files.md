---
title: Files
tags:
  - Files
---
# Reading from a file
```python
from pathlib import Path
path = Path('pi_digits.txt') # This is using relative path
contents = path.read_text()
print(contents)

contents = contents.rstrip() # Removes end of file blank line
```

## Accessing file lines
```python
contents = path.read_text()
lines = content.splitlines() # Returns a list of all lines in file
for line in lines:
	print(line)
```


## Writing to a file
```python
from pathlib import Path
path = Path('programming.txt')
path.write_text("I love programming")
```


## Writing multiple lines
```python
content = "I love programming.\n"
content += "I love creating new games.\n"
content += "I also love working with data.\n"
path.write_text(content) # If file exists, this will erase the current content
```