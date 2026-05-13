Tags: #HashTable, #dict 

----

# Building a Thesaurus for Fun and Profit, but Mainly Profit

###### When a user looks up a word in Quicksaurus,  it returns the word's most *popular* synonym, instead of *every* possible synonym.

- Since every word has an associated synonym, this is a great use case for a hash table.
- After all, a hash table is a list of paired items.

##### Representing our thesaurus using a hash table:
```python
thesaurus = {}
```

Under the hood, a hash table stores its data in a bunch of cells in a row, similar to an array. 
Each cell has a corresponding number, for example:

![[hash_table(1).png]]


#### Let's add our first entry into the hash:
```python
thesaurus["bad"] = "evil"
```

In code, our hash table now looks like this:
```python
{"bad": "evil"}
```


## How hash tables stores this data
First, the computer applies the hash function to the key.

- We will be using "multiplication" hash function described previously for demostration purposes.

BAD = 2 * 1 * 4 = 8

Since our key ("bad") hashes into 8, the computer places the value ("evil") into cell 8:

![[hash_table(2).png]]


Now, let's add another key/value pair:
```python
thesaurus["cab"] = "taxi"
```

Again, the computer hashes the key:
CAB = 3 * 1 * 2 = 6

Since the resulting value is 6, the computer stores the value ("taxi") inside cell 6.

![[hash_table(3).png]]

Lets's add one more key/value pair:
```python
thesaurus["ace"] = "star"
```


ACE hashes into 15, since ACE = 1 * 3 * 5 = 15, so "star" gets placed into cell 15:
![[hash_table(4).png]]

In code, our hash table currently looks like this:
```python
thesaurus = {"bad": "evil",
			"cab": "taxi",
			"ace": "star"}
```


##### What happens when we look up values from it ?
```python
thesaurus["bad"]
> Output: evil
```


##### The computer then executes 2 simple steps:
1. The computer hashes the key we're looking up: BAD = 2 * 1 * 4 = 8
2. Since the result is 8, the computer looks inside cell 8 and returns the value that is stored there.
	- In this case, that would be the string "evil"

Now it becomes clear why looking up a value in a hash table is typically $O(1)$:
It's a process that takes a constant amount time.

The computer hashes the key we're looking up, gets the corresponding value, and jumps to the cell with that value.


## Hash Tables vs Array

With an array, we to look up the price of a menu item, we would have to search through each cell until we found it.

For an unordered array, this would take up to $O(N)$, and for an ordered array, this would take up to $O(log N)$.

Using a hash table, however, we can now use the actual menu items as keys, allowing us to do a hash table lookup of $O(1)$.

-----

































