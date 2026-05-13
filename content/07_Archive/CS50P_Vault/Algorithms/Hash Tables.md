Data Structure: #HashTable

----

## Example
```python
menu = [
		["french fries", 0.75],
		["hamburger", 2.5],
		["hot dog", 1.5],
		["soda", 0.6]
]
```

This array contains several subarrays, and each subarray contains 2 elements.

The first element is string representing the food on the menu, and the second element represents the price of that food.

----

## Why does this matter ?
If this array were unordered, searching for the price of a given food would take $O(N)$ steps since the computer would have to perform a linear search.

If it's an *ordered* array, the computer could do a binary search, which would take $O(log N)$

### Speeding things up
While $O(log N)$ isn't bad, we can do better. In fact, we can do *much* better. 


## Using Hash Tables
- By using hash tables we can look up data in just $O (1)$.

By knowing how hash tables work under the hood and the right places to use them, we can leverage their tremendous lookup speeds in many situations.

[[Hash Tables in Action|Code Examples]]

----


# Enter the Hash Table

Here's an example of the menu as implemented with the hash table using Python:
```python
menu = {"french fries": 0.75,
	   "hamburger": 2.5,
	   "hot dog": 1.5,
	   "soda": 0.6}
```

A hash table is a list of paired values.
	The first item is known as the *key*
	The second item is known as the *value*

In a hash table, the key and value have some significant association with one another.

##### Example: "french fries" is the key, 0.75 is the value
They are paired together to indicate that french fries cost 75 cents.

#### In python you can look up a key's value using this syntax
```python
menu["french fries"]

> Output: 0.75
```

----

## Look up Efficiency
Tags: #Efficiency 

Looking up a value in a hash table has an efficiency of $O(1)$ on average, as it takes *just* one step.

----


# Hashing with Hash Functions

## Example
| A   | 1   |
| --- | --- |
| B   | 2   |
| C   | 3   |
| D   | 4   |
| E   | 5    |

According to this code,
ACE converts to 135,
CAB converts to 315,
DAB converts to 412,
and
BAD converts to 214.

- This process of taking characters and converting them to numbers is known as *hashing*.
- The code that is used to convert those letters into particular numbers is called a *hash function*


## Another Example
- Take each letter's corresponding number and return the **sum** of all the numbers.

BAD --> 2 + 1 + 4 --> 7

# Step #1:
First, BAD converts to 214

# Step #2:
We then take each of these digits and get their sum:
2 + 1 + 4 = 7


## Another Example
Another example of a hash function is to return the *product* of all letters' corresponding numbers.

This would convert the word BAD into the number 8

# Step #1:
First, BAD converts to 214

# Step #2:
We then take the product of these digits:
2 * 1 * 4 = 8

----

# Hash Function Criterion

The truth is that a hash function needs to meet only 1 criterion to be valid:
	A hash function must convert the same string to the *same* number every single time it's applied.

##### If the hash function can return inconsistent results for a given string, it's not valid.

Examples of invalid hash functions include functions that use random numbers or the current time as part of their calculation. 

With these functions, BAD might convert to 12 one time, and 106 another time.


##### With our "Multiplication" hash function, however,
BAD will *always* convert to 8. 
That's because B is always 2, A is always 1, and D is always 4.
and 2 * 1 * 4 is *always* 8.

> [!INFO]
> Note: With this hash function, DAB will *also* convert into 8 just as BAD will.
> This will actually cause some issues that we'll address later.


----



# Dealing with Collisions

- What happens if we want to add the following entry into our thesaurus ?

```python
thesaurus["dab"] = "pat"
```

First, the computer would hash the key:
DAB = 4 * 1 * 2 = 8

And then it would try to add "pat" to our hash table's cell 8:
![[hash_table(5).png]]

Uh oh. Cell 8 is already filled with "evil"

Trying to add data to a cell that is already filled is known as a *collision*.
Fortunately, there are ways around it.

## Separate Chaining
#SeparateChaining

When a collision occurs, instead of placing a *single* value in the cell, it places it in a reference to an array.

![[hash_table(6).png]]

In our example, the computer wants to add "pat" to cell 8, but it already contains "evil".
So it replaces the contents of cell 8 with an array.

![[hash_table(7).png]]

This array contains subarray where the first value is the word, and the second word is its synonym.

# Hash table lookup
If we look up:
```python
thesaurus["dab"]
```

The computer takes the following steps:
1. It hashes the key DAB = 4 * 1 * 2 = 8
2. It looks up the cell 8. The computer takes note that cell 8 contains an array if arrays rather than a single value.
3. It searches through the array linearly, looking at index 0 of each subarray until it finds the word we're looking up ("dab"). It then returns the value at index 1 of the correct subarray.


## Walkthrough

We hash DAB into 8, so the computer inspects that cell:
![[hash_table(8).png]]


Since cell 8 contains an array, we begin a linear search through each cell, starting at the first one.
It contains another array, and we inspect index 0:

![[hash_table(9).png]]


It does not contain the key we are looking for ("dab"), so we move on to the next cell:

![[hash_table(10).png]]

We found "dab", which would indicate that the value at index 1 of that subarray ("pat") is the value we're looking for.

In a scenario where the computer hits upon a cell that references an array, its search can take some extra steps, as it needs to conduct a linear search within an array of multiple values.
	- If somehow all the data ended up within a single cell of our hash table, our hash table would be no better than an array.
	- So its actually turns out that the worst-case performance for a hash table lookup is $O(N)$

- Because of this, it is critical that a hash table be designed in a way that it will have a few collisions, and therefore typically perform lookups in $O(1)$ time rather than $O(N)$ time.


# How are hash tables implemented in the real world to avoid frequent collisions.

- Ultimately, a hash table's efficiency depends on 3 factors.
	1. How much data we're storing in the hash table
	2. How many cells are available in the hash table
	3. Which hash function we're using

It makes sense why the first 2 factors are important.

If you have a lot of data to store in only a few cells, there will be many collisions and the hash tables will lose its efficiency.

# Why is Hash Function itself important for efficiency

Let's say that we're using a hash function that always produces a value that falls in the range between 1 and 9 inclusive. 

An example of this is a hash function that converts letters into their corresponding numbers, and keeps adding the resulting digits together until it ends up with a single digit.

## For Example:

PUT = 16 + 21 + 20 = 57

Since 57 contains more than 1 digit, the hash function breaks up the 57 into 5 + 7:

5 + 7 = 12

12 also contains more than 1 digit, so it breaks up the 12 into 1 +2:

1 + 2 = 3

In the end, PUT hashes into 3. This hash function by its very nature will *always* return a number 1 through 9.

![[hash_table(11).png]]

With this hash function, the computer would never even use cells 10 through 16 even though they exist. Add data would be stuffed into cells 1 through 9.

A good hash function, therefore, is one that distributes its data across all available cells.
	If we need a hash table to store just 5 values, how big should our hash table be, and what type of hash function should we use ?

If a hash table had only 5 cells, we'd need a hash function that converts keys into numbers 1 through 5.

Even if we only planned on storing 5 pieces of data, there's a good chance that there will be a collision or two, since two keys may be easily hashed to the same value.

##### However, if our hash table were to have 100 cells, and our function converts strings into numbers 1 through 100
- When storing just 5 values it would be much less likely to have any collisions since there are 100 possible cells that each of those strings might end up in.
	- Although a hash table with 100 cells is great for avoiding collisions, we'd be using up 100 cells to store just 5 pieces of data, that's a waste of memory.


# Balancing act
A good hash table strikes a balance of avoiding collisions while not consuming lots of memory.

## To accomplish this
Computer scienctists have developed the following rule of thumb:
- For every seven data elements stored in a hash table, it should have 10 cells.

## Load Factor
This ratio of data to cells is called the *load factor*. Using this terminology, we'd say that the ideal load factor is 0.7 (7 elements / 10 cells).


# Internal hash table
Luckily, most of the internals of a hash table are managed by the computer language you're using.
It decides how big the hash table needs to be, what hash function to use, and when it's time to expand the hash table.

## We can use hash tables to replace arrays

-----






