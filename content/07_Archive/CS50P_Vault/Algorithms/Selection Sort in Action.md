Algorithm: #SelectionSort 

Assume that the example array is [4, 2, 7, 1, 3], our steps would be as follow.

# 1st Passthrough
- Inspect value at index 0.
- By definition, it's the lowest value in the array that we've encountered so far  (Only value)
- Keep track of it in a variable.

![[selection_sort(2).png]]


## Step #1:
- We compare the 2 with the lowest value so far
![[selection_sort(3).png]]

- The 2 is even less than the 4, so it becomes the lowest value so far:
![[selection_sort(4).png]]


## Step #2:
- We compare the next value 7 with the lowest value so far.
- 7 > 2, so 2 remains the lowest value

![[selection_sort(5).png]]


## Step #3:
- We compare the 1 with the lowest value so far:
![[selection_sort(6).png]]

- Since the 1 is even less than the 2, the 1 becomes our new lowest value:

![[selection_sort(7).png]]

## Step #4:
- We compare the 3 to the lowest value so far, which is the 1.
- We've reached the end of the array, and we've determined that 1 is lowest value out of the entire array.
![[selection_sort(8).png]]

## Step #5:
- Since 1 is the lowest value, we swap it with whatever value is at index 0
- (The index we began this passthrough with)
![[selection_sort(9).png]]

#### We have now determined that the 1 is in its correct place within the array:
![[selection_sort(10).png]]

We are now ready to begin our 2nd passthrough

## 2nd Passthrough Setup:
- The first cell *(index 0)* is already sorted, so this passthrough begins at the next cell, which is *index 1* .
- The value at *index 1* is 2, and it the lowest value we've encountered in this passthrough so far:

![[selection_sort(11).png]]

## Step #6:
- We compare the 7 with the lowest value so far.
- The 2 is less than the 7, so the 2 remain our lowest value:

![[selection_sort(12).png]]

## Step #7:
- We compare the 4 with the lowest value so far.
- The 2 is less than the 4, so the 2 remains our lowest value.

![[selection_sort(13).png]]

## Step #8:
- We compare the 3 with the lowest value so far.
- The 2 is less than the 3, so the 2 remains our lowest value

![[selection_sort(14).png]]

- We've reached the end of the array.
- We don't need to perform any swaps in this passthrough, and we can therefore conclude that the 2 is in its correct spot.

![[selection_sort(15).png]]


# Passthrough #3:

## Setup:
- We begin at index 2, which contains the value 7

![[selection_sort(16).png]]

## Step #9:
- We compare the 4 with the 7

![[selection_sort(17).png]]

- We note that 4 is our new lowest value:

![[selection_sort(18).png]]


## Step #10:
- We encounter the 3, which is even lower than the 4

![[selection_sort(19).png]]

- 3 is now our new lowest value:

![[selection_sort(20).png]]

## Step #11:
- We've reached the end of the array, so we swap the 3 with the value that we started our passthrough at, which is the 7

![[selection_sort(21).png]]

- We now know that the 3 is in the correct place within the array:

![[selection_sort(22).png]]

##### While we can see the entire array is correctly sorted at this point, the *computer* does not know this yet, so it must begin a fourth passthrough:

# Passthrough #4

## Setup:
- We begin the passthrough with index 3


## Step #12:
- We compare the 7 with the 4:

![[selection_sort(23).png]]

- The 4 remains the lowest value we've encountered in this passthrough so far, so we don't need any swaps and we know it's in the correct place.
- Since all the cells besides the last one are correctly sorted, that must mean that the last cell is also in the correct order, and our entire array is properly sorted:

![[selection_sort(24).png]]

----
