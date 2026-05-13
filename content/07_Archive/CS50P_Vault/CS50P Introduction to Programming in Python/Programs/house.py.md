Tags: [[Lecture 1 - Conditionals]]




## Using match
```python
name = input("What's your name?")

if name == "Harry":
	print("Gryffindor")
elif name == "Hermione":
	print("Gryffindor")
elif name == "Ron":
	print("Gryffindor")
elif name == "Draco":
	print("Slytherin")
else:
	print("Who?")

< Input: Harry
> Output: Gryffindor

< Input: Padma
> Output: Who?


----------------------------------------------------------------------------------------


name = input("What's your name?")

if name == "Harry"or name == "Hermione" or name == "Ron":
	print("Gryffindor")
elif name == "Draco":
	print("Slytherin")
else:
	print("Who?")

< Input: Hermione
> Output: Gryffindor

< Input: Ron
> Output: Gryffindor


----------------------------------------------------------------------------------------


name = input("What's your name?")

match name:
	case "Harry":
		print("Gryffindor")
	case "Hermione"
		print("Gryffindor")
	case "Ron":
		print("Gryffindor")
	case "Draco":
		print("Slytherin")
	case _:
		print("Who?")




< Input: Hermione
> Output: Gryffindor

< Input: Padma
> Output: Who?

----------------------------------------------------------------------------------------


name = input("What's your name?")

match name:
	case "Harry"| "Hermione" | "Ron":
		print("Gryffindor")
	case "Draco":
		print("Slytherin")
	case _:
		print("Who?")

< Input: Hermione
> Output: Gryffindor

< Input: Harry
> Output: Gryffindor

```