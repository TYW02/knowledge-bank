Algorithm: #SelectionSort


----
## Steps to follow

## Step 1:
- Check each cell of the array from left to right to determine which value is least.
- Keep in a variable the **lowest** value (Track the index)
- If we encounter a cell that contains a value that is even 1 less than the one in our variable.
- Replace it so that the variable now points to the new index.

![[selection_sort(1).png]]


## Step 2:
- Once we determined whic index contains the lowest value, we swap that index with the value we began the passthrough with.
- This would be index 0 in the first passthrough, index 1 in the 2nd passthrough, and so on and so forth.


## Step 3:
- Repeat Step [[#Step 1:|1]] and [[#Step 2:|2]] until all the data is sorted

----


# Selection Sort Implemented
Code Example: #Code_Example 
[[Selection Sort in Action]]
```python
def selectionSort(arr):
	for i in range(len(arr)):
		for j in range(i, len(arr)):
			if arr[j] < arr[i]:
				arr[j], arr[i] = arr[i], arr[j]
	return arr
```
## Breaking it down line by line

```python
for i in range(len(arr)):
	for j in range(i, len(arr))
```

This helps you pass through the arr, `i` is the sorted index and `j` is you comparing if there is a smaller value compared to the current `i`




# Efficiency of Selection Sort
Efficiency: #Efficiency 

Selection Sort contains 2 types of steps: comparisons and swaps.

That is, we compare each element with the lowest number we've encountered in each passthrough, and we swap the lowest number into its correct position.

#### Example: Array containing 5 elements, we had to make a total of ten comparisons

| Passthrough #| # of comparisons |
|----|----|
| 1 | 4 Comparisons |
| 2 | 3 Comparisons |
| 3 | 2 Comparisons |
| 4 | 1 Comparisons |

So that's a total of 4 + 3 + 2 + 1 = 10 Comparisons

We'd say that for **N** elements, we make (N - 1) + (N - 2) + (N - 3) .. + 1 Comparisons.

#### As for swaps

We only need to make a maximum of one swap per passthrough.

This is because in each passthrough, we make either one or zero swaps, depending on whether the lowest number of that passthrough is already in the correct position.

#### Compared to Bubble Sort
[[07_Archive/CS50P_Vault/Algorithms/Bubble Sort]]

Contrast this with Bubble Sort, where in a worst-case scenario --an array in descending order-- we have to make a swap for *each* and *every* comparison.

### Side-by-Side Comparison [Bubble Sort] vs [Selection Sort]

| N Elements | Max # of steps in [[07_Archive/CS50P_Vault/Algorithms/Bubble Sort]] | Max # of steps in [[Selection Sort]] |
| ---- | ---- | ----|
| 5 | 20 | 14 (10 Comparisons + 4 Swaps) |
| 10 | 90 | 54 (45 Comparisons + 9 Swaps) |
| 20 | 380 | 199 (180 Comparisons + 19 Swaps) |
| 40 | 1560 | 819 (780 Comparisons + 39 Swaps) |
| 80 | 6320 | 3239 (3160 Comparisons + 79 Swaps) |

- From this comparison, it's clear that Selection Sort contains about half the number of steps that Bubble Sort does, indicating that Selection Sort is twice as fast.



## In Big O Notation
Selection is described in Big O as $O(N^2)$, just like [[07_Archive/CS50P_Vault/Algorithms/Bubble Sort]].





