
```python
x = torch.ones((10))
y = x.view((2,5))
z = x.view((-1,5))  # -1 is a joker (inferred dimension)
y = x.reshape((2,5))
```

> [!important] What it does:
> `view` and `reshape` change tensor shape **without** copying data, `-1` infers the missing dimension.

> [!note] If you change
> `(2, 5)` -> `(5, 2)` changes shape. 
> - Take the total number of elements you have (e.g. **10**)
> - Divide by the **KNOWN** number in your `view` that gives you the number if `-1`
> - (10 / 5 = 2)
> - Therefore, x.view((-1, 5)), gives shape (2, 5)


## Transpose
```python
x = torch.randn(2, 3)
a = x.transpose(0, 1)  # shape [3, 2]


# Create a 3D tensor with shape (2, 3, 4) 
x = torch.randn(2, 3, 4) 

# Swap the first (0) and second (1) dimensions 
# The resulting shape becomes (3, 2, 4) 
y = torch.transpose(x, 0, 1) print(y.shape) # Output: torch.Size([3, 2, 4])
```

> [!important] How it works
> This basically means swap dim `0` with dim `1`
> - So swap 2 with 3


## Permute
```python
x = torch.randn(2, 3, 5)
print(torch.permute(x, (2, 0, 1)).shape)  # [5, 2, 3]
```

> [!important] How it works
> - Here we take position `2` which is **5** and place it at the `0` index
> - Position `0` which is **2** place at `1`
> - Position `1` which is **3** place at `2`
> - Same to the rest.

## Squeeze
```python
x = torch.zeros([1, 2, 3])
x = x.squeeze(0)  # shape [2, 3]
```

> [!important] How it works
> Removes dimensions of size **1**
> - If a dimension has size greater than 1, `squeeze` will completely ignore it and leave the tensor unchanged.

## Unsqueeze
```python
x = torch.zeros([2, 3])
x = x.unsqueeze(1)  # shape [2, 1, 3]
```

> [!important] Inserts a dimension of size 1 at the specified position
> - Here we are inserting a dimension at index 1 which is where the current `3` is so 
> - It will become \[2, 1, 3\]


## Concatenation
```python
x = torch.zeros([2, 1, 3])
y = torch.zeros([2, 3, 3])
z = torch.zeros([2, 2, 3])
w = torch.cat([x, y, z], dim=1)  # shape [2, 6, 3]
```

> [!important] What it does
> Concatenates along dimension 1.
> - Total size = 1+3+2 = 6
> - **IMPORTANT**: You can only get the SIZE by adding them together **NOT** the data
> - If you change: `dim=0` it will concatenate along that dimension (Requires other dims to **MATCH**)




























