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
def insertionSort(arr):
	for i in range(1, len(arr)):
		for j in range(i, 0, -1):
			if arr[j - 1] > arr[j]:
				arr[j - 1], arr[j] = arr[j], arr[j - 1]
	return arr
```

## Breaking it down line by line
We start by defining the first for loop
```python
for i in range(1, len(arr))
```

This line helps us get all the elements from the 2nd element to the end.
We want to start from the 2nd element because our `j` will be behind our `i` counter.

```python
for j in range(i, 0, -1)
```
This is the j counter travelling backwards we start where `i` is because anything to the RIGHT of `i` has not been sorted.

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

## *Big O Notation only takes into account the highest order of N*

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


