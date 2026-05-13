Tags: [[Lecture 2 - Loops]]



```python
students = ["Hermione", "Harry", "Ron"]

print(students[0])
print(students[1])
print(students[2])

> Output: Hermione
> Harry
> Ron 

----------------------------------------------------------------------------------------

students = ["Hermione", "Harry", "Ron"]

for student in students:
	print(student)

> Output: Hermione
> Harry
> Ron 

----------------------------------------------------------------------------------------

students = ["Hermione", "Harry", "Ron"]

for i in range(len(students)):
	print(students[i])
	
> Output: Hermione
> Harry
> Ron 

----------------------------------------------------------------------------------------

students = ["Hermione", "Harry", "Ron"]

for i in range(len(students)):
	print(i + 1, students[i])
	
> Output: 1 Hermione
> 2 Harry
> 3 Ron 

```

^11c88a


## Using dict
```python
students = {"Hermione": "Gryffindor", 
			"Harry": "Gryffindor",
			"Ron": "Gryffindor",
			"Draco": "Slytherin"}

print(students["Hermione"])
print(students["Harry"])
print(students["Ron"])
print(students["Draco"])

> Output: Gryffindor
> Gryffindor
> Gryffindor
> Slytherin

----------------------------------------------------------------------------------------

students = {"Hermione": "Gryffindor", 
			"Harry": "Gryffindor",
			"Ron": "Gryffindor",
			"Draco": "Slytherin"}

for student in students:
	print(students, students[student], sep=",")

> Output: Hermione, Gryffindor
> Harry, Gryffindor
> Ron, Gryffindor
> Draco, Slytherin

```


## Enhanced Dictionary
```python
students = [
	{"name": "Hermione", "house": "Gryffindor", "patronus": "Otter"},
	{"name": "Harry", "house": "Gryffindor", "patronus": "Stag"},
	{"name": "Ron", "house": "Gryffindor", "patronus": "Jack Russell Terrier"},
	{"name": "Draco", "house": "Slytherin", "patronus": None}
]

for student in students:
	print(students["name"], students["house"], students["patronus"], sep", ")

> Output:
> Hermione, Gryffindor, Otter
> Harry, Gryffindor, Stag
> Ron, Gryffindor, Jack Russell Terrier
> Draco, Slytherin, None
```



