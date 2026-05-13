


# Scalars
#Scalar 

Most everyday mathematics consists of manipulating numbers one at a time. Formally, we call these values _scalars_.


For example, the temperature in Palo Alto is a balmy degrees Fahrenheit. If you wanted to convert the temperature to Celsius you would evaluate the expression $c = \frac{5}{9}(f-32)$, setting f to 72 . In this equation, the values 5, 9, and 32 are constant scalars. The variables c and f in general represent unknown scalars.

Just remember that the expression $x \in r$ is a formal way to say that is a real-valued scalar. The symbol $\in$ (pronounced “in”) denotes membership in a set. For example, $x,y \in0,1$ indicates that x and y are variables that can only take values 0 or 1.

```python
x = torch.tensor(3.0)
y = torch.tensor(2.0)

x + y, x * y, x / y, x**y

# (tensor(5.), tensor(6.), tensor(1.5000), tensor(9.))
```


# Vectors
#Vector 

For current purposes, you can think of a vector as a fixed-length array of scalars.

When vectors represent examples from real-world datasets, their values hold some real-world significance. For example, if we were training a model to predict the risk of a loan defaulting, we might associate each applicant with a vector whose components correspond to quantities like their income, length of employment, or number of previous defaults.

```python
x = torch.arange(3)
x

# tensor([0, 1, 2])
```


We can refer to an element of a vector by using a subscript. For example $x_2$, denotes the second element of . Since $x_2$ is a scalar, we do not bold it. By default, we visualize vectors by stacking their elements vertically.

![[Pasted image 20250817213828.png]]

```python
x[2]

# tensor(2)
```
We access a tensor's elements via indexing

To indicate that a vector contains elements $n$, we write $x \in R^n$ . Formally, we call the _dimensionality_ of the vector. In code, this corresponds to the tensor’s length, accessible via Python’s built-in `len` function.

We can also access the length via the `shape` attribute. The shape is a tuple that indicates a tensor’s length along each axis. Tensors with just one axis have shapes with just one element.
```python
len(x)
# 3

x.shape
# torch.Size([3])
```



# Matrices



The expression $A \in R^{m x n}$ indicates that a matrix A contains m x n real-valued scalars, arranged as m rows and n columns.

To refer to an individual element, we subscript both the row and column indices, e.g., $a_{ij}$ is the value that belongs to A’s $i^{th}$ row and $j^{th}$ column:
![[Pasted image 20250817214512.png]]

In code, we represent a matrix $A \in R^{mxn}$ by a 2nd-order tensor with shape (m,n). We can convert any appropriately sized m x n tensor into an m x n matrix by passing the desired shape to `reshape`:
```python
A = torch.arange(6).reshape(3, 2)
A

# tensor([[0, 1],
#        [2, 3],
#        [4, 5]])

A.T
# tensor([[0, 2, 4],
#        [1, 3, 5]])
```

Symmetric matrices are the subset of square matrices that are equal to their own transposes: $A =A^T$ . The following matrix is symmetric:
```python
A = torch.tensor([[1, 2, 3], [2, 0, 4], [3, 4, 5]])
A == A.T

# tensor([[True, True, True],
#        [True, True, True],
#        [True, True, True]])
```


# Tensor
#Tensor 

While you can go far in your machine learning journey with only scalars, vectors, and matrices, eventually you may need to work with higher-order tensors. Tensors give us a generic way of describing extensions to $n^{th}$-order arrays

```python
torch.arange(24).reshape(2, 3, 4)

# tensor([[[ 0,  1,  2,  3],
#         [ 4,  5,  6,  7],
#         [ 8,  9, 10, 11]],

#        [[12, 13, 14, 15],
#         [16, 17, 18, 19],
#         [20, 21, 22, 23]]])
```


# Basic Properties of Tensor Arithmetic

Scalars, vectors, matrices, and higher-order tensors all have some handy properties. For example, elementwise operations produce outputs that have the same shape as their operands.
```python
A = torch.arange(6, dtype=torch.float32).reshape(2, 3)
B = A.clone() # Assign a copy of A to B by allocating new memory
A, A + B

# (tensor([[0., 1., 2.],
#         [3., 4., 5.]]),
# tensor([[ 0.,  2.,  4.],
#         [ 6.,  8., 10.]]))
```

The elementwise product of two matrices is called their Hadamard product.
```python
A * B

# tensor([[ 0.,  1.,  4.],
#        [ 9., 16., 25.]])
```

Adding or multiplying a scalar and a tensor produces a result with the same shape as the original tensor. Here, each element of the tensor is added to ( or multiplied by) the scalar.
```python
a = 2
X = torch.arange(24).reshape(2, 3, 4)
a + X, (a * X).shape

# (tensor([[[ 2,  3,  4,  5],
#          [ 6,  7,  8,  9],
#          [10, 11, 12, 13]],

#         [[14, 15, 16, 17],
#          [18, 19, 20, 21],
#          [22, 23, 24, 25]]]),
# torch.Size([2, 3, 4]))
```



# Reduction

Often, we wish to calculate the sum of a tensor's elements. To express the sum of the elements in a vector x of length n, we write $\sum_{i=1}^{n} x_i$ There is a simple function for it:
```python
x = torch.arange(3, dtype=torch.float32)
x, x.sum()

# (tensor([0., 1., 2.]), tensor(3.))
```

To express sums over the elements of tensors of arbitrary shape, we simply sum over all its axes.
For example, the sum of the elements of an m x n matrix A could be written $\sum_{i=1}^{m}\sum_{j=1}^{n}a_{ij}$
```python
A.shape, A.sum()
# (torch.Size([2, 3]), tensor(15.))
```


By default, invoking the sum function _reduces_ a tensor along all of its axes, eventually producing a scalar. 
Our libraries also allow us to specify the axes along which the tensor should be reduced. To sum over all elements along the rows (axis 0), we specify `axis=0` in `sum`. Since the input matrix reduces along axis 0 to generate the output vector, this axis is missing from the shape of the output.
```python
A.shape, A.sum(axis=0).shape
# (torch.Size([2, 3]), torch.Size([3]))
```

Specifying `axis=1` will reduce the column dimension (axis 1) by summing up elements of all the columns.
```python
A.shape, A.sum(axis=1).shape
# (torch.Size([2, 3]), torch.Size([2]))
```

Reducing a matrix along both rows and columns via summation is equivalent to summing up all the elements of the matrix.
```python
A.sum(axis=[0, 1]) == A.sum()  # Same as A.sum()
# tensor(True)
```

A related quantity is the _mean_, also called the _average_. We calculate the mean by dividing the sum by the total number of elements. Because computing the mean is so common, it gets a dedicated library function that works analogously to `sum`.
```python
A.mean(), A.sum() / A.numel()
# (tensor(2.5000), tensor(2.5000))
```

Likewise, the function for calculating the mean can also reduce a tensor along specific axes.
```python
A.mean(axis=0), A.sum(axis=0) / A.shape[0]
# (tensor([1.5000, 2.5000, 3.5000]), tensor([1.5000, 2.5000, 3.5000]))
```


# Non-Reduction Sum

Sometimes it can be useful to keep the number of axes unchanged when invoking the function for calculating the sum or mean. This matters when we want to use the broadcast mechanism.
```python
sum_A = A.sum(axis=1, keepdims=True)
sum_A, sum_A.shape

# (tensor([[ 3.],
#         [12.]]),
# torch.Size([2, 1]))
```


For instance, since `sum_A` keeps its two axes after summing each row, we can divide `A` by `sum_A` with broadcasting to create a matrix where each row sums up to 1.
```python
A / sum_A
# tensor([[0.0000, 0.3333, 0.6667],
#        [0.2500, 0.3333, 0.4167]])
```

If we want to calculate the cumulative sum of elements of `A` along some axis, say `axis=0` (row by row), we can call the `cumsum` function. By design, this function does not reduce the input tensor along any axis.
```python
A.cumsum(axis=0)
# tensor([[0., 1., 2.],
#        [3., 5., 7.]])
```



# Dot Products

So far, we have only performed elementwise operations, sums, and averages. And if this was all we could do, linear algebra would not deserve its own section.

One of the most fundamental operations is the dot product. Given two vectors $x, y \in R^d$, their _dot product_ $x^Ty$(also known as _inner product_,(x, y) ) is a sum over the products of the elements at the same position: $x^Ty=\sum_{i=1}^dx_iy_i$.
```python
y = torch.ones(3, dtype = torch.float32)
x, y, torch.dot(x, y)

# (tensor([0., 1., 2.]), tensor([1., 1., 1.]), tensor(3.))
```
Equivalently, we can calculate the dot product of two vectors by performing an elementwise multiplication followed by a sum:
```python
torch.sum(x * y)
# tensor(3.)
```

Dot products are useful in a wide range of contexts. For example, given some set of values, denoted by a vector $x\in R^n$, and a set of weights, denoted by $w \in R^n$, the weighted sum of the values in x according to the weights w could be expressed as the dot product $x^Tw$. When the weights are nonnegative and sum to 1, i.e.,($\sum_{i=1}^{n}w_i=1$) , the dot product expresses a _weighted average_. After normalizing two vectors to have unit length, the dot products express the cosine of the angle between them. Later in this section, we will formally introduce this notion of _length_.


# Matrix-Vector Products

Now that we know how to calculate dot products, we can begin to understand the _product_ between an m x n matrix A and an n-dimensional vector x. To start off, we visualize our matrix in terms of its row vectors

![[Pasted image 20250819215010.png]]

where each $a^T_{i}\in R^n$ is a row vector representing the $i^{th}$ row of the matrix A

The matrix–vector product Ax is simply a column vector of length m, whose $i^{th}$ element is the dot product $a^T_ix$:
![[Pasted image 20250819215322.png]]

We can think of multiplication with a matrix $A\in R^{mxn}$ as a transformation that projects vectors from $R^n$ to $R^m$. These transformations are remarkably useful. For example, we can represent rotations as multiplications by certain square matrices. Matrix–vector products also describe the key calculation involved in computing the outputs of each layer in a neural network given the outputs from the previous layer.

To express a matrix–vector product in code, we use the `mv` function. Note that the column dimension of `A` (its length along axis 1) must be the same as the dimension of `x` (its length). Python has a convenience operator `@` that can execute both matrix–vector and matrix–matrix products (depending on its arguments). Thus we can write `A@x`.
```python
A.shape, x.shape, torch.mv(A, x), A@x
# (torch.Size([2, 3]), torch.Size([3]), tensor([ 5., 14.]), tensor([ 5., 14.]))
```



# Matrix-Matrix Multiplication

Once you have gotten the hang of dot products and matrix-vector products, then matrix-matrix multiplication should be straightforward.

Say that we have two matrices $A \in R^{nxk}$ and $B \in R^{kxm}$
![[Pasted image 20250819215824.png]]

Let $a^T_i \in R^k$ denote the row vector representing the $i^{th}$ row of the matrix A and let $b_j \in R^k$ denote the column vector from the $j^{th}$ column of the matrix B:
![[Pasted image 20250819220008.png]]

To form the matrix product $C \in R^{nxm}$ , we simply compute each element $c_{ij}$as the dot product between the $i^{th}$ row of A and the $j^{th}$ column of B, i.e., $a^T_ib_j$ :
![[Pasted image 20250819220148.png]]

We can think of the matrix–matrix multiplication AB as performing m matrix–vector products or m x n dot products and stitching the results together to form an n x m matrix. In the following snippet, we perform matrix multiplication on `A` and `B`. Here, `A` is a matrix with two rows and three columns, and `B` is a matrix with three rows and four columns. After multiplication, we obtain a matrix with two rows and four columns.
```python
B = torch.ones(3, 4)
torch.mm(A, B), A@B

# (tensor([[ 3.,  3.,  3.,  3.],
#         [12., 12., 12., 12.]]),
# tensor([[ 3.,  3.,  3.,  3.],
#         [12., 12., 12., 12.]]))
```
The term _matrix–matrix multiplication_ is often simplified to _matrix multiplication_, and should not be confused with the Hadamard product.


# Norms

Some of the most useful operators in linear algebra are _norms_. Informally, the norm of a vector tells us how _big_ it is. For instance, the norm measures the (Euclidean) length of a vector. Here, we are employing a notion of _size_ that concerns the magnitude of a vector’s components (not its dimensionality).

A norm is a function ||.|| that maps a vector to a scalar and satisfies the following three properties:

![[Pasted image 20250819220524.png]]
```python
u = torch.tensor([3.0, -4.0])
torch.norm(u)

# tensor(5.)
```


![[Pasted image 20250819220628.png]]
```python
torch.abs(u).sum()

# tensor(7.)
```


![[Pasted image 20250819220714.png]]
```python
torch.norm(torch.ones((4, 9)))

# tensor(6.)
```

While we do not want to get too far ahead of ourselves, we already can plant some intuition about why these concepts are useful. In deep learning, we are often trying to solve optimization problems: _maximize_ the probability assigned to observed data; _maximize_ the revenue associated with a recommender model; _minimize_ the distance between predictions and the ground truth observations; _minimize_ the distance between representations of photos of the same person while _maximizing_ the distance between representations of photos of different people. These distances, which constitute the objectives of deep learning algorithms, are often expressed as norms.









































