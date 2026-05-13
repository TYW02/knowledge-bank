Algorithm: #BubbleSort

Assume that we wanted to sort the array [4, 2, 7, 1, 3]. 
It's currently out of order, and we want to produce an array containing the same values in the correct, ascending order.


# Passthrough #1

This is our starting array:
![[bubble_sort(4).png]]

### Step #1: First, we compare the 4 and the 2. They're out of order:
![[bubble_sort(5).png]]

### Step #2: So we swap them:
![[bubble_sort(6).png]]

### Step #3: Next, we compare the 4 and 7:
![[bubble_sort(7).png]]

They're in the correct order, so we don't need to perform any swaps.

### Step #4: We now compare the 7 and the 1:
![[bubble_sort(8).png]]


### Step #5: They're out of order, so we swap them
![[bubble_sort(9).png]]
![[bubble_sort(10).png]]


### Step #6: We compare the 7 and the 3:
![[bubble_sort(11).png]]


### Step #7: They're out of order, so we swap them:
![[bubble_sort(12).png]]


## End of Passthrough #1

### What happened here ?
We now know for a fact that the 7 is in its correct position within the array.
We basically pass through the array and shifted the largest element to the end.



#### Since we made at least 1 swap during this passthrough, we need to conduct another one.




# Passthrough #2:

The 7 is already in the correct position


### Step #8: We begin by comparing the 2 and the 4
![[bubble_sort(13).png]]

They're in the correct order, so we can move on.


### Step #9: We compare the 4 and the 1
![[bubble_sort(14).png]]

They're out of order, so we swap them.
![[bubble_sort(15).png]]


### Step #11: We compare the 4 and 3:
![[bubble_sort(16).png]]

They're out of order, so we swap them.

![[bubble_sort(17).png]]

## End of Passthrough #2

### What happened here ?
We don't have to compare the 4 and 7 because we know that the 7 is already in its correct position from [[#End of Passthrough 1|Passthrough #1]].

Now we also know that 4 is bubbled up to its correct position as well.

This concludes our 2nd passthrough.

Since we made at least 1 swap during this passthrough, we need to conduct another one.

---


# Passthrough #3

## Step #13: We compare the 2 and 1:
![[bubble_sort(18).png]]

They're out of order, so we swap them

## Step #14: We compare 2 and the 3
![[bubble_sort(19).png]]

They're in the correct order, so we don't need to swap them.

## What happened ?
We now know that 3 has bubbled up to its correct spot.

Since we made at least 1 swap this passthrough, we need to perform another one.

----

# Passthrough #4:

## Step #15: We compare the 1 and the 2
![[bubble_sort(20).png]]

Since they're in order, we don't need to swap. We can end this passthrough, since all the remaining values are alreadt correctly sorted.

Now that we've made a passthrough that didn't require any swaps, we know that our array is completely sorted:
![[bubble_sort(21).png]]

---

