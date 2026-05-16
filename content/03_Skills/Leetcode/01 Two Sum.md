---
title: Two Sum
tags:
  - Array
---
Given an array of integers `nums` and an integer `target`, return _indices_ of the 2 numbers such that they add up to `target`

Assume that each input have exactly 1 solution, and you may not use the same element twice.

### Example 1
```python
# Input: nums = [2, 7, 11, 15], target = 9
# Output: [0, 1] 
```
Because nums[0] + nums[1] == 9 we return [0, 1]
### Example 2
```python
# Input: nums = [3, 2, 4], target = 6
# Output: [1, 2] 
```
### Example 3
```python
# Input: nums = [3, 3], target = 6
# Output: [0, 1] 
```

## Thought Process
We have to find a combination of elements that make up the target value.
If we take the target value - the elements in the array we can check if the remaining value exists in the array and if it does, we can return the position of each corresponding element.



# Solution
```python
def twoSum(nums, target):
	ans = []
	for i in range(len(nums)):
		find = target - nums[i]
		for j in range(i + 1, len(nums)):
			if nums[j] == find:
				return [i, j]
```