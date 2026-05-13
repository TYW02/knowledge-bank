Algorithm: #InsertionSort 

Assume that the example array is [4, 2, 7, 1, 3], our steps would be as follow.


# 1st Passthrough
Inspect the value at index 1. This happens to contain the value 2:
![[insertion_sort(5).png]]

## Setup:
- We temporarily removed the 2, and keep it inside a variable called *temp_value*.
- We represent this value by shifting it above the rest of the array.



## Step #1:
We compare the 4 to the *temp_value*, which is 2:
![[insertion_sort(6).png]]


## Step #2:
Since 4 is greater than 2, we shift the 4 to the right:
![[insertion_sort(7).png]]

There's nothing left to shift, as the gap is now at the left end of the array.


## Step #3:
We insert the *temp_value* back into the array, completing our first passthrough:



# 2nd Passthrough

## Setup:
- In the 2nd passthrough, we temporarily remove the value at index 2.
- In this case, the *temp_value* is 7.

![[insertion_sort(9).png]]

## Step #4:
- We compare the 4 to the *temp_value*
![[insertion_sort(10).png]]

- 4 is lower, so we won't shift it.
- Since we reached a value that is less than the *temp_value*, this shifting phase is over.


## Step #5:
We insert the *temp_value* back into the gap, ending the 2nd passthrough


# 3rd Passthrough

## Setup:
We temporarily remove the 1, and store it in *temp_value*:

![[insertion_sort(11).png]]


## Step #6:
We compare the 7 to the *temp_value*:
![[insertion_sort(12).png]]

## Step #7:
7 is greater than 1, so we shift the 7 to the right:
![[insertion_sort(13).png]]


## Step #8:
We compare the 4 to the *temp_value*

![[insertion_sort(14).png]]

## Step #9:
4 is greater than 1, so we shift it as well

![[insertion_sort(15).png]]


## Step #10
We compare the 2 to the *temp_value*

![[insertion_sort(16).png]]

## Step #11:
The 2 is greater, so we shift it

![[insertion_sort(17).png]]


## Step #12:
The gap has reached the left end of the array, so we insert the *temp_value* into the gap, concluding this passthrough

![[insertion_sort(18).png]]


# Passthrough #4


## Setup
We temporarily remove the value from index 4, making it our *temp_value*. This is the value 3

![[insertion_sort(19).png]]


## Step #13:
We compare the 7 to the *temp_value*

![[insertion_sort(20).png]]

## Step #14:
The 7 is greater, so we shift the 7 to the right

![[insertion_sort(21).png]]


## Step #15:
We comapre the 4 to the *temp_value*

![[insertion_sort(22).png]]


## Step #16:
The 4 is greater than the 3, so we shift the 4

![[insertion_sort(23).png]]


## Step #17:
We compare the 2 to the *temp_value* 2 is less than 3, so our shifting phase is complete

![[insertion_sort(24).png]]


## Step #18:
We insert the *temp_value* back into the gap
![[insertion_sort(25).png]]

Our array is now fully sorted
![[insertion_sort(26).png]]

----
