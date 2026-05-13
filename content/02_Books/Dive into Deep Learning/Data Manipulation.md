

## Generally, there are 2 important things we need to do with data
1. Acquire them
2. Process them once they are inside the computer



# Getting Started

PyTorch provides a variety of functions for creating new tensors prepopulated with values. For example, by invoking `arange(n)`, we can create a vector of evenly spaced values, starting at 0 (included) and ending at `n` (not included)
```python
x = torch.arange(12, dtype=torch.float32)
x
# tensor([ 0.,  1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 11.])
```

Each of these values is called an _element_ of the tensor. The tensor `x` contains 12 elements. We can inspect the total number of elements in a tensor via its `numel` method.

We can access a tensor’s _shape_ (the length along each axis) by inspecting its `shape` attribute. Because we are dealing with a vector here, the `shape` contains just a single element and is identical to the size.
```python
x.numel()
# 12
x.shape
# torch.Size([12])
```


We can change the shape of a tensor without altering its size or values, by invoking `reshape`. For example, we can transform our vector `x` whose shape is (12,) to a matrix `X` with shape (3, 4). This new tensor retains all elements but reconfigures them into a matrix. Notice that the elements of our vector are laid out one row at a time and thus `x[3] == X[0, 3]`.
```python
X = x.reshape(3, 4)
X

# tensor([[ 0.,  1.,  2.,  3.],
#        [ 4.,  5.,  6.,  7.],
#        [ 8.,  9., 10., 11.]])
```


#zeros #ones
Practitioners often need to work with tensors initialized to contain all 0s or 1s. We can construct a tensor with all elements set to 0 and a shape of (2, 3, 4) via the `zeros` function.
```python
torch.zeros((2, 3, 4))

# tensor([[[0., 0., 0., 0.],
#          [0., 0., 0., 0.],
#          [0., 0., 0., 0.]],

#         [[0., 0., 0., 0.],
#          [0., 0., 0., 0.],
#         [0., 0., 0., 0.]]])

torch.ones((2, 3, 4))

# tensor([[[1., 1., 1., 1.],
#          [1., 1., 1., 1.],
#          [1., 1., 1., 1.]],

#         [[1., 1., 1., 1.],
#          [1., 1., 1., 1.],
#         [1., 1., 1., 1.]]])
```


We often wish to sample each element randomly (and independently) from a given probability distribution. For example, the parameters of neural networks are often initialized randomly. The following snippet creates a tensor with elements drawn from a standard Gaussian (normal) distribution with mean 0 and standard deviation 1.
#randn
```python
torch.randn(3, 4)

# tensor([[ 0.1351, -0.9099, -0.2028,  2.1937],
#         [-0.3200, -0.7545,  0.8086, -1.8730],
#         [ 0.3929,  0.4931,  0.9114, -0.7072]])
```


Finally, we can construct tensors by supplying the exact values for each element by supplying (possibly nested) Python list(s) containing numerical literals. Here, we construct a matrix with a list of lists, where the outermost list corresponds to axis 0, and the inner list corresponds to axis 1.
```python
torch.tensor([[2, 1, 4, 3], [1, 2, 3, 4], [4, 3, 2, 1]])

# tensor([[2, 1, 4, 3],
#         [1, 2, 3, 4],
#         [4, 3, 2, 1]])
```


# Indexing and Slicing
#Indexing #Slicing

As with Python lists, we can access tensor elements by indexing (starting with 0). To access an element based on its position relative to the end of the list, we can use negative indexing. 

Finally, we can access whole ranges of indices via slicing (e.g., `X[start:stop]`), where the returned value **includes** the first index (`start`) _but **not the last**_ (`stop`). Finally, when only one index (or slice) is specified for a k-order tensor, it is applied along axis 0. 

Thus, in the following code, `[-1]` selects the last row and `[1:3]` selects the second and third rows.
```python
X[-1], X[1:3]

# (tensor([ 8.,  9., 10., 11.]),
#  tensor([[ 4.,  5.,  6.,  7.],
#          [ 8.,  9., 10., 11.]]))
```

Beyond reading them, we can also _write_ elements of a matrix by specifying indices.
```python
X[1, 2] = 17
X

# tensor([[ 0.,  1.,  2.,  3.],
#         [ 4.,  5., 17.,  7.],
#         [ 8.,  9., 10., 11.]])
```


If we want to assign multiple elements the same value, we apply the indexing on the left-hand side of the assignment operation. For instance, `[:2, :]` accesses the first and second rows, where `:` takes all the elements along axis 1 (column). While we discussed indexing for matrices, this also works for vectors and for tensors of more than two dimensions.
```python
X[:2, :] = 12
X

# tensor([[12., 12., 12., 12.],
#         [12., 12., 12., 12.],
#        [ 8.,  9., 10., 11.]])
```

> [!NOTE]
> X[:2, :] = 12 
> This needs to be broken down first we are indexing :2 and : 
> :2 means from 0 to 1 which is our row value
> : means all of our col value then set all to 12



# Operations

Now that we know how to construct tensors and how to read from and write to their elements, we can begin to manipulate them with various mathematical operations.

These apply a standard scalar operation to each element of a tensor.

```python
torch.exp(x)

# tensor([162754.7969, 162754.7969, 162754.7969, 162754.7969, 162754.7969,
#         162754.7969, 162754.7969, 162754.7969,   2980.9580,   8103.0840,
#          22026.4648,  59874.1406])
```


```python
x = torch.tensor([1.0, 2, 4, 8])
y = torch.tensor([2, 2, 2, 2])
x + y, x - y, x * y, x / y, x ** y

# (tensor([ 3.,  4.,  6., 10.]),
#  tensor([-1.,  0.,  2.,  6.]),
#  tensor([ 2.,  4.,  8., 16.]),
#  tensor([0.5000, 1.0000, 2.0000, 4.0000]),
#  tensor([ 1.,  4., 16., 64.]))
```


In addition to elementwise computations, we can also perform linear algebraic operations, such as dot products and matrix multiplications.
#DotProduct #MatrixMultiplication #Concat


We can also _concatenate_ multiple tensors, stacking them end-to-end to form a larger one. We just need to provide a list of tensors and tell the system along which axis to concatenate.

>[!NOTE]
>The example below shows what happens when we concatenate two matrices along rows (axis 0) instead of columns (axis 1).


```python
X = torch.arange(12, dtype=torch.float32).reshape((3,4))
Y = torch.tensor([[2.0, 1, 4, 3], [1, 2, 3, 4], [4, 3, 2, 1]])
torch.cat((X, Y), dim=0), torch.cat((X, Y), dim=1)

# (tensor([[ 0.,  1.,  2.,  3.],
#          [ 4.,  5.,  6.,  7.],
#          [ 8.,  9., 10., 11.],
#          [ 2.,  1.,  4.,  3.],
#          [ 1.,  2.,  3.,  4.],
#          [ 4.,  3.,  2.,  1.]]),
#  tensor([[ 0.,  1.,  2.,  3.,  2.,  1.,  4.,  3.],
#          [ 4.,  5.,  6.,  7.,  1.,  2.,  3.,  4.],
#          [ 8.,  9., 10., 11.,  4.,  3.,  2.,  1.]]))
```
We can see that the first output’s axis-0 length (6) is the sum of the two input tensors’ axis-0 lengths (3+3); while the second output’s axis-1 length (8) is the sum of the two input tensors’ axis-1 lengths (4+4).

> [!NOTE]
> When concatenating dim 0 lengthens the tensor 
> While dim 1 widens it


Sometimes, we want to construct a binary tensor via _logical statements_. Take `X == Y` as an example. For each position `i, j`, if `X[i, j]` and `Y[i, j]` are equal, then the corresponding entry in the result takes value `1`, otherwise it takes value `0`.
```python
X == Y

# tensor([[False,  True, False,  True],
#         [False, False, False, False],
#         [False, False, False, False]])

X.sum()

# tensor(66.)
```


# Broadcasting

By now, you know how to perform elementwise binary operations on two tensors of the same shape. Under certain conditions, even when shapes differ, we can still perform elementwise binary operations by invoking the _broadcasting mechanism_

(i) expand one or both arrays by copying elements along axes with length 1 so that after this transformation, the two tensors have the same shape; (ii) perform an elementwise operation on the resulting arrays.
```python
a = torch.arange(3).reshape((3, 1))
b = torch.arange(2).reshape((1, 2))
a, b

# (tensor([[0],
#          [1],
#          [2]]),
#  tensor([[0, 1]]))
```


Since `a` and `b` are and matrices, respectively, their shapes do not match up. Broadcasting produces a larger matrix by replicating matrix `a` along the columns and matrix `b` along the rows before adding them elementwise.
```python
a + b

# tensor([[0, 1],
#         [1, 2],
#         [2, 3]])
```

So basically, it turns
```python
(tensor([[0], 
		[1],
		[2]]))

(tensor([[0,0],
		[1,1],
		[2,2]]))

# then it adds with [0, 1] which gives you 

tensor([[0, 1],
        [1, 2],
        [2, 3]])
```


# Conversion to Other Python Objects
#from_numpy

Converting to a NumPy tensor (`ndarray`), or vice versa, is easy. The torch tensor and NumPy array will share their underlying memory, and changing one through an in-place operation will also change the other.
```python
A = X.numpy()
B = torch.from_numpy(A)
type(A), type(B)

# (numpy.ndarray, torch.Tensor)
```


To convert a size-1 tensor to a Python scalar, we can invoke the `item` function or Python’s built-in functions.
```python
a = torch.tensor([3.5])
a, a.item(), float(a), int(a)

# (tensor([3.5000]), 3.5, 3.5, 3)
```



