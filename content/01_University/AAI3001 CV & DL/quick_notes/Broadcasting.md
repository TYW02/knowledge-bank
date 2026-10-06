
# Main Idea

> [!important] Main Idea
> Line up shape from the **RIGHT**, treat **missing dimensions as size 1**, and each dimensions **MUST** either **match** or be **1**.


## The Rule

> [!note] Given 2 shapes, Pytorch:
> 1. Pads the shorter shape with `1`s on the **left** until both have the same number of dimensions.
> 2. Compares dimensions from **right to left**.
> 3. For each dimension, it is **compatible** if:
> 	- the sizes are **equal**, or
> 	- one of them is `1`.
> 4. The resulting dimension is **the larger** of the two.
> 5. If any dimension is **incompatible**, you get a ==🔴broadcasting error==

### Example
```python
a.shape = (3, 1)
b.shape = (1, 4)
```
### Align
```python
a: 3  1
b: 1  4
```

Compare right to left:
- `1` vs `4` -> OK, result: `4`
- `3` vs `1` -> OK, result: `3`
### Result shape
```python
(3, 4)
```


### Examples that work
```python
(3, 1) + (1, 4)        -> (3, 4)

(5, 3, 1) + (3, 4)     -> (5, 3, 4)
# b is padded to (1, 3, 4)

(2, 3) + (3,)          -> (2, 3)
# b is padded to (1, 3)

() + (2, 3)            -> (2, 3)
# scalar broadcasts to anything

(4, 1) + (4,)          -> (4, 4)
# b is padded to (1, 4); often surprising!
```
# Examples that FAIL
```python
(3,) + (4,)            -> error
# 3 vs 4

(3, 4) + (2, 4)        -> error
# rightmost 4 == 4, but next 3 vs 2

(2, 3) + (2,)          -> error
# b becomes (1, 2), then 3 vs 2 fails

(5, 3, 1) + (2, 3, 4)  -> error
# right: 1 vs 4 OK, 3 vs 3 OK, 5 vs 2 fails
```


# What to watch out for

## 1. Right-alignment, not left-alignment

- Missing dimensions are added on the **LEFT**, not the right
- For image `(N, C, H, W)`, as per-channel bias should be shaped like:
```python
bias.shape == (C, 1, 1)

x.shape    = (N, C, H, W)
bias.shape = (C, 1, 1)
# result   = (N, C, H, W)
```


## 2. Vector vs Column vector confusion
- If you have a matric `(N, M)` and want to add a vector of length `N` to each row, use:
```python
v.shape = (N, 1)
x + v   # (N, M) + (N, 1) -> (N, M)

x.shape = (N, M)
v.shape = (N,)
x + v   # (N, M) + (1, N) -> usually error unless N == M
```

> [!note]
> If you use `v.shape = (N,)`, it becomes `(1, N)` and will align against `M`, usually causing an error or doing the wrong thing.

> [!success] Fix with
> ```python
> v = v[:, None]   # or v.unsqueeze(1)
> ```

## `matmul` / `@` has extra rules

- For `torch.matmul`, broadcasting applies mainly to **batch dimensions**. The last 2 dimensions must still be **matrix-compatible**
```python
(2, 3, 4) @ (2, 4, 5) -> (2, 3, 5)
```
- The inner matrix dimension `4` and `4` must **match**

# Practice Questions

> [!question] For each pair of shapes, will broadcasting succeed ? If yes, what is the result shape ? If no, why not ?
> - a. `(3, 1)` and `(1, 4)`
> - b. `(5, 3, 1)` and `(3, 4)`
> - c. `(4, 1)` and `(4,)`
> - d. `(2, 3)` and `(2,)`
> - e. `(2, 3, 4)` and `(3, 1)`

> [!question] What happens here ?
> ```python
> x = torch.ones(3, 1)
> y = torch.ones(1, 4)
> x += y
> ```

> [!question] You have `x` of shape `(N, M)` and `v` of shape `(N,)`. You want to add `v` to every row of `x`. What should you write? Why does `x + v` usually fail?

- Do shapes `(8, 1, 6, 1)` and `(7, 1, 5)` broadcast? If yes, what is the result shape?
- Do shapes `(3, 2)` and `(3, 1, 2)` broadcast? If yes, what is the result shape?
- Do shapes `(2, 3)` and `(2, 3, 4)` broadcast? If yes, what is the result shape?

# Answer

- a. **Yes** → `(3, 4)`
- b. **Yes** → `(5, 3, 4)`  
    `(3, 4)` becomes `(1, 3, 4)`
- c. **Yes** → `(4, 4)`  
    `(4,)` becomes `(1, 4)`. This often surprises people because it is not elementwise.
- d. **No**  
    `(2,)` becomes `(1, 2)`. Then `3` vs `2` fails at the last dimension.
- e. **Yes** → `(2, 3, 4)`  
    `(3, 1)` becomes `(1, 3, 1)`.

The broadcast result is `(3, 4)`, but `x` has shape `(3, 1)`. In-place operations cannot resize the destination tensor.

- **Yes** → `(8, 7, 6, 5)`.  
    `(7, 1, 5)` becomes `(1, 7, 1, 5)`.
- **Yes** → `(3, 3, 2)`.  
    `(3, 2)` becomes `(1, 3, 2)`.
- **No.**  
    `(2, 3)` becomes `(1, 2, 3)`. Then the last dimension `3` vs `4` fails.








































