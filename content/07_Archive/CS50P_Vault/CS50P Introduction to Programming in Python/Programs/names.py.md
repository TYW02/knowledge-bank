Tags: [[Lecture 6 - File IO]]


# Starting Program
```python
name = input("What's your name? ")
print(f"hello, {name}")
```




# Using list
```python
names  = []

for _ in range(3):
	names.append(input("What's your name? "))

for name in sorted(names):
	print(f"hello, {name}")

< What's your name? Hermione
< Harry
< Ron

> hello, Harry
> hello, Hermione
> hello, ron
```
The computer is unable to store the values in the list for long term.
So when you rerun the program it is gone.



# Saving in File I/O
```python
name = input("What's your name? ")

file = open("names.txt", "w")
file.write(name)
file.close()

< What's your name? Hermione
```
>[!INFO]
>You should see Hermione in a file called names.txt
>
>If you run this code multiple times with different names only the most recent one will be saved.



## Appending names in file
```python 
name = input("What's your name? ")

file = open("names.txt", "a")
file.write(name)
file.close()

< What's your name? Hermione
```
> [!INFO]
> Here since you are using "a" which appends the items into the file, you should see multiple names being appended to the file.
> 
> However, they will appear as
> 
> HermioneHarryRon


## Fixing the appending names
```python
name = input("What's your name? ")

file = open("names.txt", "a")
file.write(f"{name}\n")
file.close()

< What's your name? Hermione
```
> [!INFO]
> Here, the file should look much cleaner and easier to read



## Automatically open and close files using with
```python
name = input("What's your name? ")

with open("names.txt", "a") as file:
	file.write(f"{name}\n")

< What's your name? Hermione
```



## Reading from file
```python
with open("names.txt", "r") as file:
	lines = file.readlines() # Reads all the line in file

for line in lines:
	print("hello,", line)

> hello, Harry

hello, Ron

hello, Hermione

```
This example's output is not the cleanest


## Making it look better
```python
with open("names.txt", "r") as file:
	lines = file.readlines() # Reads all the line in file

for line in lines:
	print("hello,", line.rstrip())

> hello, Harry

hello, Ron

hello, Hermione
```


## Making it faster
```python
with open("names.txt", "r") as file:
	for line in file:
		print("hello,", line.rstrip())

> hello, Hermione
> hello, Harry
> hello, Ron
```
Printing issue has been fixed here


## Sorting the output in order
```python
names = []

with open("names.txt") as file:
	for line in file:
		names.append(line.rstrip()) # You are appending to memory here and not a file

for name in sorted(names):
	print(f"hello, {name}")

> hello, Draco
> hello, Harry
> hello, Hermione
> hello, Ron
```


## Another way to sort 
```python
with open("names.txt") as file:
	for line in sorted(file):
		print("hello,", line.rstrip())

> hello, Draco
> hello, Harry
> hello, Hermione
> hello, Ron
```























