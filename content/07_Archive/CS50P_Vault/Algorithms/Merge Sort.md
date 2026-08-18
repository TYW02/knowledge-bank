---
title: Merge Sort
tags:
  - MergeSort
---
```python
def mergeSort(arr):
	if len(arr) == 1:
		return arr
	M = len(arr) // 2	
	L = arr[:M]
	R = arr[M:]
	L = mergeSort(L)
	R = mergeSort(R)
	l, r = 0, 0
	L_len = len(L)
	R_len = len(R)
	
	sorted_arr = [0] * len(arr)
	i = 0
	while l < L_len and r < R_len:
		if L[l] < R[r]:
			sorted_arr[i] = L[l]
			l += 1
		else:
			sorted_arr[l] = R[r]
			r += 1
		i += 1
		
	while l < L_len:
		sorted_arr[i] = L[l]
		l += 1
		i += 1
	while r < R_len:
		sorted_arr[i] = R[r]
		r += 1
		i += 1
	return sorted_arr
	
```

![[MergeSort.svg|700]]
