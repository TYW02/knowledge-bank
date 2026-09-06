---
title: Tensor Operations
---
> [!IMPORTANT]
> Most operations in PyTorch are NOT in-place. Meaning that the resulting tensor is a NEW tensor and does not share the underlying data with other tensors.

```python
t = torch.rand(3, 3)

# All of these are the same, t remains unaffected
torch.add(t, t)
t.add(t)
t + t 

# Here t will change
t.add_(t)
```


> [!In-Place Operations]-
> They are still available in PyTorch and they are more efficient since they never require to perform deep copies of the data. They are normally recognized by a trailing `_`


# Basic Operations & Broadcasting
> [!Element-wise]
> Basic math (+, -, \*, /, \*\*) are applied **element-wise**.
> For example:
> `x*y` is a tensor with the same size.

> [!Broadcasting]
> Allows PyTorch to perform operations on tensors of **different** shapes. 

```python
x = torch.tensor([[1, 2], [3, 4]], dtype=torch.float32)
y = torch.tensor([[5, 6], [7, 8]], dtype=torch.float32)

print(x + y) # Element-wise sum
print(x + 4.2) # Broadcasting
```

```python
m = torch.arange(12).reshape(4, 3) # Shape: (4, 3)
v = torch.tensor([100, 0, 200]) # Shape: (3)
n = m + v # Broadcast: (4, 3) + (3) = (4, 3)

```


### Question
> Given two vectors $x∈R^n$ and $y∈R^m$, compute the differences between all possible pairs of their elements, and organize these differences in a matrix $Z∈R^{n×m}$:
> $z_{ij}=x_{i}−y_{j}$

```python
x = torch.tensor([1, 2, 3])
y = torch.tensor([4, 5])
```

> [!Solution]-
> ```python
> x = torch.tensor([1, 2, 3])
> y = torch.tensor([4, 5])
> z = x.unsqueeze(-1) - y
> ```


## Broadcastable Tensors
2 tensors are "Broadcastable" if:
- Each tensor has at least 1 dimension
- When iterating over the dimension sizes, starting at the trailing dimension, the dimension **size** must either be **equal**, **one of them is 1** or **one of them does not exist**.

## Broadcasting Rules
1. If input tensor have different **ranks**, singleton dimensions are prepended to the shape of the smaller one until it has the same rank as the other
2. The size in each dimension of the **output shape** is the maximum size in that dimension between the 2 tensors
3. An input can be used in the computation if its size in a particular **dimension either matches the output size** in that dimension, or is a **singleton** dimension
4. If an input has a dimension size of 1 in its shape, the first data entry in that dimension will be used for all calculations along that dimension.

### Visualization Example
- `m` has shape `[4, 3]`
- `n` has shape `[3,]`
```python
n = m + v

# tensor([[100,   1, 202],
#        [103,   4, 205],
#        [106,   7, 208],
#        [109,  10, 211]]) <shape: torch.Size([4, 3])> <dtype: torch.int64>
```

> [!What Happened]
> - `v` has less dims than `m` so a dimension of `1` is **prepended** -> `v` is now `[1, 3]`
> - Output Shape will be `[max(1, 4), max(3, 3)] = [4, 3]`
> - dim 1 of `v` matches exactly `3`; dim 0 is `1` so we can use the first data entry in that dimension each time any row is accessed. This is like converting `v` from `[1, 3]` to `[4, 3]` by stacking the repeated row 4 times.


# Non-elementwise Operations
```python
x = torch.tensor([[1, 2, 3], [4, 5, 6]], dtype=torch.float32)
torch.sum(x) # This returns a scalar value of 18
torch.mean(x, dim=0) # This returns value [2, 3, 4]
# dim = 0 refers to the oth index of the shape [2, 3]

torch.prod(x, dim=1) # Product of each row
values, indices = torch.max(x, dim=0) # max of each col
values, indices = torch.max(x, dim=1) # max of each row
```

## Exercise
- Compute the mean of the value along its diagonal
```python
x = torch.rand(4, 4)
# tensor([[0.6323, 0.3489, 0.4017, 0.0223],
#        [0.1689, 0.2939, 0.5185, 0.6977],
#        [0.8000, 0.1610, 0.2823, 0.6816],
#        [0.9152, 0.3971, 0.8742, 0.4194]]) <shape: torch.Size([4, 4])> <dtype: torch.float32>
```

> [!Solution]-
> ```python
> a = torch.mean(x[torch.arange(x.shape[0]), x[torch.arange(x.shape[1])])
> b = torch.sum(torch.eye(x.shape[0]) * x) / x.shape[0]
> c = torch.trace(x) / x.shape[0]
> d = torch.mean(torch.diag(x))
> ```


### `torch.clamp()`
> Used to restrict all elements in a tensor to a specified minimum and maximum range

```python
torch.clamp(input, min=None, max=None, *, out=None) -> Tensor

# Create a sample 1D tensor 
x = torch.tensor([1.5, -2.3, 5.0, 0.5, -0.1]) 
# Clamp values to be between 0.0 and 1.0 
clamped_x = torch.clamp(x, min=0.0, max=1.0) print(clamped_x) 
# Output: tensor([1.0000, 0.0000, 1.0000, 0.5000, 0.0000])

```

> [!NOTE]
> `torch.clip()` is an alias for this function.


## Matrix Multiplication
```python
x = torch.tensor([[1, 2], [3, 4], [5, 6]]) # Shape" [3, 2]
y = torch.tensor([[1, 2], [2, 1]]) # Shape [2, 2]
```


```python
torch.matmul(x, y)
x @ y # Same as above
torch.mm(x, y) # Only for rank-2 tensor
x.mm(y) # Tensor method
torch.einsum('ik, kj -> ij', (x, y)) # Einsum notation
```


## Dot Product
```python
x = torch.tensor([1, 2, 3])
y = torch.tensor([4, 5, 6])

# We want to perform
(1 * 4) + (2 * 5) + (3 * 6) = 32
```

```python
torch.dot(x, y) # Commonly used
x.dot(y) # Commonly used
x @ y
torch.einsum('i, i ->', (x, y))
# Read it as 
# Iterate with i along x, i along y
# compute product at each iteration
# sum the product and return a scalar (-> means return a scalar)
```

## Batch matrix multiplication
```python
x = torch.tensor([[[1, 2], [3, 4], [5, 6]], [[1, 2], [3, 4], [5, 6]]]) #Shape: (2, 3, 2)
y = torch.tensor([[[1, 2], [2, 1]], [[1, 2], [2, 1]]]) #Shape: (2,2,2)
```

```python
torch.bmm(x, y)
x @ y
torch.einsum('bik, bkj -> bij', (x,y))
```


## Broadcast matrix multiplication
```python
x = torch.tensor([[[1, 2], [3, 4], [5, 6]], [[1, 2], [3, 4], [5, 6]]]) #Shape: (2,3,2)
y = torch.tensor([[1, 2], [2, 1]]) #Shape: (2,2)
```

```python
torch.matmul(x, y) # always uses the last 2 dimensions
# So here its doing (3, 2) and (2, 2) -> (2, 3, 2)
x @ y # same as above
```


# einsum Operations
#einsum
```python
a = torch.arange(6).reshape(2, 3)
```

## Matrix Transpose
```python
b = torch.einsum('ij -> ji', a)
```


## Sum
```python
b = torch.einsum('ij ->', a)
```


## Column Sum
```python
b = torch.einsum('ij -> j', a)
```

## Matrix-vector Multiplication
```python
a = torch.arange(6).reshape(2, 3)
b = torch.arange(3)
c = torch.einsum('ik, k -> i', [a,b])
```

## Matrix-Matrix Multiplication
```python
a = torch.arange(6).reshape(2, 3)
b = torch.arange(15).reshape(3, 5)
c = torch.einsum('ik, kj -> ij', [a, b])
```

## Dot Product
```python
a = torch.arange(3)
b = torch.arange(3, 6)
c = torch.einsum('i, i ->', [a, b])
```


## Point-Wise Multiplication
```python
a = torch.arange(6).reshape(2, 3)
b = torch.arange(6, 12).reshape(2, 3)
c = torch.einsum('ij, ij -> ij', [a, b])
```

## Outer Product
```python
a = torch.arange(3)
b = torch.arange(3, 7)
c = torch.einsum('i, j -> ij', [a, b])

# OR
torch.outer(a, b)
# OR
a[:, None] * b[None, :]
```

## Batch Matrix Multiplication
```python
a = torch.randn(2, 2, 5)
b = torch.randn(2, 5, 3)
c = torch.einsum('bik, bkj -> bij', [a, b])
```