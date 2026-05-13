Tags: [[Lecture 6 - File IO]]


## Reading csv file
```python
with open("students.csv") as file:
	for line in file:
		row = line.rstrip().split(",")
		print(f"{row[0]} is in {row[1]})

> Hermione is in Gryffindor
> Harry is in Gryffindor
> Ron is in Gryffindor
> Draco is in Slytherin
```


## Making code cleaner
```python
with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		print(f"{name} is in {house})

> Hermione is in Gryffindor
> Harry is in Gryffindor
> Ron is in Gryffindor
> Draco is in Slytherin
```


## Sorting the list
```python 
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		students.append(f"{name} is in {house}")

for student in sorted(students):
	print(student)

> Draco is in Slytherin
> Harry is in Gryffindor
> Hermione is in Gryffindor
> Ron is in Gryffindor
```


## Better version
```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {}
		student["name"] = name
		student["house"] = house
		students.append(student)

for student in students:
	print(f"{student['name']} is in {student['house']}")

> Hermione is in Gryffindor
> Harry is in Gryffindor
> Ron is in Gryffindor
> Draco is in Slytherin
```


## Cleaning up code
```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {"name": name, "house": house}
		students.append(student)

for student in students:
	print(f"{student['name']} is in {student['house']}")

> Hermione is in Gryffindor
> Harry is in Gryffindor
> Ron is in Gryffindor
> Draco is in Slytherin
```


## Sorting dictionary
```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {"name": name, "house": house}
		students.append(student)

def get_name(student):
	return student["name"]

def get_house(student):
	return student["house"]

for student in sorted(students, key=get_name):
	print(f"{student['name']} is in {student['house']}")

# Sorted by Name
> Draco is in Slytherin
> Harry is in Gryffindor
> Hermione is in Gryffindor
> Ron is in Gryffindor

# Sorted by House
> Hermione is in Gryffindor
> Harry is in Gryffindor
> Ron is in Gryffindor
> Draco is in Slytherin
```


## Lambda Functions
```python
students = []

with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {"name": name, "house": house}
		students.append(student)



for student in sorted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is in {student['house']}")

> Draco is in Slytherin
> Harry is in Gryffindor
> Hermione is in Gryffindor
> Ron is in Gryffindor
```



## Using csv library
```python
import csv

students = []

with open("students.csv") as file:
	reader = csv.reader(file)
	for name, home in reader:
		students.append({"names": name, "home": home})



for student in sorted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is from {student['home']}")

> Draco is from Malfoy Manor
> Harry is from Number four, Privet Drive
> Ron is from The Burrow
```



## Using csv.DictReader
```python
import csv

students = []

with open("students.csv") as file:
	reader = csv.Dictreader(file)
	for row in reader:
		students.append({"names": row["name"], "home": row["home"]})



for student in sorted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is from {student['home']}")

> Draco is from Malfoy Manor
> Harry is from Number four, Privet Drive
> Ron is from The Burrow
```

>[!INFO]
>Your students.csv should look like this <br /><br /> name, home <br /> Harry, Number Four, Privet Drive <br /> Ron, The Burrow <br /> Draco, Malfoy Manor


## Writing data in csv (csv.writer)
```python
import csv

name = input("What's your name? ")
home = input("Where's your home? ")

with open("students.csv", "a") as file:
	writer = csv.writer(file)
	writer.writerow([name, home])

< What's your name? Harry
< Where's your home? Number Four, Privet Drive 
```

>[!INFO]
>In students.csv you should see the following: <br /><br /> name,home <br /> Harry, "Number Four, Privet Drive"


## Using csv.DictWriter
```python
import csv

name = input("What's your name? ")
home = input("Where's your home? ")

with open("students.csv", "a") as file:
	writer = csv.Dictwriter(file, fieldnames=["name", "home"])
	writer.writerow({"name": name, "home": home})

< What's your name? Harry
< Where's your home? Number Four, Privet Drive 
```

>[!INFO]
>In students.csv you should see the following: <br /><br /> name,home <br /> Harry, "Number Four, Privet Drive"


























