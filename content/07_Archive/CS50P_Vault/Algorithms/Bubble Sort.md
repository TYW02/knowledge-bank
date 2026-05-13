Algorithm: #BubbleSort 

##  What is bubble sort ?
- It is a basic sorting algorithm




### Why is it called bubble sort ?
In each passthrough, the highest unsorted value "bubbles" up to its correct position



## Steps to follow

## 1. Point to 2 consecutive items in the array.
We start at the very beginning of the array and point to its first 2 items.
	Compare the 1st item with the 2nd one.
	![[bubble_sort(1).png]]


## 2.  If the 2 items are out of order
Left value greater than right
Swap them
	![[bubble_sort(2).png]]
(If they already happen to be in the correct order, do nothing for this step.)


## 3. Move the "pointers" one cell to the right:
	![[bubble_sort(3).png]]
Repeat Step [[#1. Point to 2 consecutive items in the array.|1]] and [[#2. If the 2 items are out of order|2]] until we reach the end of the array or any items that have already been sorted.

## 4. Repeat steps 1 through 3 until we have a round in which we didn't have to make any swaps. This means the array is in order.

Each time we repeat steps 1 through 3 is know as a *passthrough*. That is, we "passed through" the primary steps of the algorithm, and will repeat the same process until the array is fully sorted.

----



# Bubble Sort Implemented
Code Example: #Code_Example
[[Bubble Sort in Action]]

```python
def bubble_sort(list):
	unsorted_until_index = len(list) - 1
	sorted = False
	
while not sorted:
	sorted = True
	for i in range(unsorted_until_index):
		if list[i] > list[i + 1]:
			sorted = False
			list[i], list[i + 1] = list[i + 1], list[i]
		unsorted_until_index = unsorted_until_index - 1

list = [65, 55, 45, 35, 25, 15, 10]
bubble_sort(list)
print list

> Output: [10, 15, 25, 35, 45, 55, 65]
```

## Breaking it down line by line


```python
# Gives you the last index of the list
# Would return 6 if following above example
unsorted_until_index = len(list) - 1
```

We keep track of up to which index is still unsorted with the *unsorted_until_index* variable.
At the beginning, the array is totally unsorted, so we initialize this variable to be the final index in the array.

Basically for i in range to the last index

```python
sorted = False
```

We also create a **sorted** variable that will allow us to keep track whether the array is fully sorted. Of course, when our code first runs, it isn't

```python
while not sorted:
	sorted = True
```

We begin a **while** loop that will last as long as the array is not sorted. Next, we preliminarily establish **sorted** to be **True**. 

We'll change this back to **False** as soon as we have to make any swaps.

If we get through an entire passthrough without having to make any swaps, we'll know that the array is completely sorted.

(Whenever a swap is made change sorted to **False** but if the if condition is not met then list is sorted)

```python
for i in range(unsorted_until_index):
	if list[i] > list[i+1]:
		sorted = False
		list[i], list[i+1] = list[i+1], list[i]
```

Within the **while** loop, we begin a *for* loop that starts from the beginning of the array and goes until the index that has not yet been sorted.

Within this loop, we compare every pair of adjacent values, and swap them if they're out of order. We also change **sorted** to **False** if we have to make a swap.

```python
unsorted_until_index = unsorted_until_index - 1
```

By this line of code, we've completed another passthrough, and can safely assume that the value we've bubbled up to the right is now in its correct position.

Because of this, we decrement the **unsorted_until_index** by 1, since the index it was already pointing to is now sorted.

Each round of the **while** loop represents another passthrough, and we run it until we know that our array is fully sorted.



# The Efficiency of Bubble Sort
Efficiency: #Efficiency

The Bubble Sort algorithm contains two kinds of steps: 
- Comparisons: two numbers are compared with one another to determine which is greater. 
- Swaps: two numbers are swapped with one another in order to sort them.

### How many comparisons take place in Bubble Sort
For example our array has 5 elements, you can see that in our first passthrough, we had to make 4 comparisons between sets of 2 numbers.

In the 2nd passthrough, we had to make only 3 comparisons. This is because we didn't have to compare the final 2 numbers, since we knew that the final number was in the correct spot due to the first passthrough.

In the 3rd passthorugh, we made 2 comparisons, and in our fourth passthrough, we made just 1 comparison.

#### So that's:
4 + 3 + 2 + 1 = 10 comparisons

To put it more generally, we'd say that for N elements, we make 
(N -1) + (N - 2) + (N -3) ... + 1 Comparisons

---

### How many swaps take place in Bubble Sort

#### Worst-Case scenario
Array is not just randomly shuffled, but sorted in descending order (opposite of what we want) 

We'd actually need a swap for each comparison. So we'd have 10 comparisons and 10 swaps in such a scenario for a total for 20 steps.

#### An Array with 10 elements in reverse order
9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 = 45 comparisons, and another 45 swaps = 90 Swaps

Notice the inefficiency here, As the number of elements increase, the number of steps grows exponentially.

We can see this clearly with the following table:
 | N data elements | Max # of steps|
 |-----|-----|
 | 5 | 20 |
 | 10 | 90 |
 | 20 | 380 |
 | 40 | 1560 |
 | 80 | 6320 |

If you look precisely at the growth of steps as N increases, you'll see that it's growing by approximately $N^2$ .

 | N data elements | # of Bubble Sort Steps| $N^2$ |
 |-----|-----|----|
 | 5 | 20 | 25 |
 | 10 | 90 | 100 |
 | 20 | 380 | 400 |
 | 40 | 1560 | 1600 |
 | 80 | 6320 | 6400 |

## In Big O Notation

We would say that Bubble Sort has an efficiency of $O(N^2)$

Officially: in an $O(N^2)$ algorithm, for N data elements, there are roughly $N^2$ steps.

$O(N^2)$ is considered to be a relatively inefficient algorithm, since as the data increases, the steps increase dramatically.
![[bubble_sort(22).png]]

Note how $O(N^2)$ curves sharply upward in terms of number of steps as the data grows
Compare this with $O(N)$, which plots along a simple, diagonal line.

#### Last Note
$O(N^2)$ is also referred to as *quadratic time*.

 

