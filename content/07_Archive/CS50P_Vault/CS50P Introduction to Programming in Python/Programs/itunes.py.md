Tags: [[Lecture 4 - Libraries]]




# Itunes API
```python
import requests
import sys

if len(sys.argv) != 2:
	sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit1&term=" + sys.argv[1])

print(response.json())



```


## Using json library
```python
import json
import requests
import sys

if len(sys.argv) != 2:
	sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=1&term=" + sys.argv[1])

print(json.dumps(response.json(), indent=2))


```



## Making it look nice
```python
import json
import requests
import sys

if len(sys.argv) != 2:
	sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=1&term=" + sys.argv[1])

o = response.json()

# Looks through the results list from the API response then print Key value trackName
for result in o["results"]:
	print(result["trackName"])

> Output: Say It Ain't So
```


