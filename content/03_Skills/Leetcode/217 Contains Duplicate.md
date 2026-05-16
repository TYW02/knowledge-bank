---
tags:
  - Sets
---
Given an integer array `nums`, return `true` if any value appear **at least twice** in the array, and return `false` if every element is distinct.

### Example 1
```python
# Input: nums = [1, 2, 3, 1]
# Output = true
```
The element 1 occurs at the indices 0 and 3

### Example 2
```python
# Input: nums = [1, 2, 3, 4]
# Output = false
```
All elements are distinct

### Example 3
```python
# Input: nums = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]
# Output = true
```


# Thought Process
We should use a set here as they cannot have duplicate values, so if a value is already in the set we can return true as that means that number is already in the set.

```python
def containsDuplicate(nums):
	hashset = set()
	for num in nums:
		if num in hashset:
			return True
		else:
			hashset.add(num)
	return False
```
