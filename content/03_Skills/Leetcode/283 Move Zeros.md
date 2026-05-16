---
title: Move Zeros
---
Given an integer array `nums`, move all `0` to the end of it while maintaining the relative order of the non-zero elements.
You must do this in-place without making a copy of the array

### Example 1
```python
# Input: nums = [0, 1, 0, 3, 12]
# Output: [1, 3, 12, 0, 0]
```

### Example 2
```python
# Input: nums = [0]
# Output: [0]
```


# Solution

## Thought Process
We have to move all the non-zero elements forward and zeros at the back. To achieve this, whenever we see a number that is not `0` we shift it forward 
```python
def moveZeros(nums):
	index = 0
	for i in range(len(nums)):
		if i != 0:
			nums[i], nums[index] = nums[index], nums[i]
			index += 1
```
