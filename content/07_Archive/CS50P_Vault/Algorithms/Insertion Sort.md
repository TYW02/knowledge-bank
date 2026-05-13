Algorithm: #InsertionSort 


----

## Steps to follow

## Step 1:
In the first passthrough, we temporarily remove the value at index 1 (2nd cell) and store it in a temporary variable.

This will leave a gap at that index, since it contains no value:

![[insertion_sort(1).png]]

In Subsequent passthroughs, we remove the values at the subsequent indexes.


## Step 2:
We then begin a **shifting phase**, where we take each value to the left of the gap, and compare it to the value in the temporary variable:

![[insertion_sort(2).png]]

If the value to the left of the gap is greater than the temporary variable, we shift that value to the right:

![[insertion_sort(3).png]]

As we shift the values to the right, inherently, the gap moves leftwards.

As soon as we encounter a value that is lower than the temporarily removed value, or we reach the left end of the array, this shifting phase is over.

## Step 3:
We then insert the temporarily removed value into the current gap:

![[insertion_sort(4).png]]

## Step 4:
We repeat steps 1 through 3 until the array is fully sorted.

----



# Insertion Sort Implemented
Code Example: #Code_Example 
[[Insertion Sort in Action]]


```python
def insertion_sort(array):
	for index in range(1, len(array)):
		position = index
		temp_value = array[index]

		while position > 0 and array[position - 1] > temp_value:
			array[position] = array[position - 1]
			position = position - 1
		array[position] = temp_value
```


## Breaking it down line by line
```python
for index in range(1, len(array))
```
- We start loop at index 1 that runs through the entire array.
- The current index is kept in the variable *index*

Next, we mark a **position** at whatever **index** currently is. We also assign the value at that index to the variable *temp_value*


```python
while position > 0 and array[position - 1] > temp_value:
	array[position] = array[position - 1]
	position = position - 1
```

> [!INFO]
> We use position > 0, because python allows negative value for position

We then begin an inner **while** loop. We check whether the value to the left of *position* is greater than the *temp_value*.

If it is, we then use **array[position] = array[position - 1]** to shift that left value one cell to the right, and then decrement *position* by one.

We then check whether the value to the left of the new *position* is greater than *temp_value*, and keep repeating this process until we find a value that is less than the *temp_value*



```python
array[position] = temp_value
```

Finally, we drop the *temp_value* into the gap within the array.

---


## My Version (Code Breakdown)
```python
array = [4, 2, 7, 1, 3]

def insertion_sort(array):
	for i in range(1, len(array)):
		value_to_sort = array[i]
		while array[i - 1] > value_to_sort and i > 0:
			array[i - 1], array[i] = array[i], array[i - 1]
			i = i - 1

insertion_sort()
print(array)
```

## Breaking it down line by line


```python
for i in range(1, len(array)):
	value_to_sort = array[i]
```

The for loop is used to get the second item in the list onwards till the last item.
- We start from the second item because the left item from the 1st would be nothing

Then we store the 2nd item in a variable to be compared, in this case it is ==2==



```python
while array[i - 1] > value_to_sort and i > 0:
	array[i - 1], array[i] = array[i], array[i - 1]
	i = i - 1
```

> [!INFO]
> We use i > 0 here because python allows negative **i** which is not what we want 

The while loop here is to compare the 1st item and 2nd item.
- If the 1st item [i -1] is ==bigger== than the 2nd item [value_to_sort] 
	- Then we swap both their positions

-----

# Efficiency of Insertion Sort
Efficiency: #Efficiency 

There are 4 types of steps that occur in Insertion Sort
- Removals
- Comparisons
- Shifts
- Insertions

### Comparisons
- A Comparison takes place each time we compare a value to the left of the gap with the *temp_value*

##### Worst-Case Scenario
- Array is sorted in reverse order

1 + 2 + 3 + ... + N - 1 Comparison

In our example of an array containing 5 elements, that's a maximum of:
1 + 2 + 3 + 4 = 10 Comparison

For an array containing ten elements, there would be:
1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 = 45 Comparisons. 
(For an array containing twenty elements, there would be a total of 190 comparisons, and so on.)


##### Formula for Comparison
$N^2 / 2$ Comparisons
- $10^2 / 2 = 50$
- $20^2 / 2 = 200$



### Shifts
- Shifts occur each time we move a value 1 cell to the right.
- When an array is sorted in reverse order, there will be as many shifts as there are comparisons, since every comparison will force us to shift a value to the right.

### Adding up Shifts and Comparisons for Worst-Case
$N^2 / 2$ Comparisons + $N^2 / 2$  Shifts = $N^2$ Steps



### Removing and Inserting 
- They happen once per passthrough.
- Since there are always $N - 1$ Passthroughs, we can conclude that there are N -1 removals and N - 1 insertions

----




# In Big O Notation
![[insertion_sort(27).png]]

> [!INFO]
> Big O ignores constants so we can simplify it to.

$O(N^2 + N)$

## *Big o Notation only takes into account the highest order of N*

Example:
If an algorithm takes $N^4$ + $N^3$ + $N^2$ + $N$ steps, we only consider $N^4$ to be significant.

| N | $N^2$ | $N^3$ | $N^4$ |
|---|---|---|---|
|2 |4|8|16
|5|25|125|625|
|10|100|1,000|10,000|
|100|10,000|1,000,000|100,000,000|
|1,000|1,000,000|1,000,000,000|1,000,000,000,000|

- As N increases $N^4$ becomes so much more significant than any other order of N.


