

## Convolution vs Cross-correlation
| Feature                 | Convolution                   | Cross-Correlation          |
| ----------------------- | ----------------------------- | -------------------------- |
| Mathematical Definition | Slides a flipped kernel as is | Slides kernel              |
| Implementation          | Standard maths theory         | Common in DL libraries     |
| Performance             | Similar if weights learned    | Similar if weights learned |

# Output Shape & Parameter Counting

## Output Shape

For conv layer with input `W` or `H`, kernel size `k`, stride `s`, padding `p` and dilation `d`
$$
W_{out} = \lfloor \frac{W+2p - k_{eff}}{s} \rfloor + 1
$$
Where:
$$
k_{eff} = (k - 1) \cdot d + 1
$$

### Worked example 1: basic conv

Input `32×32`, `Conv3×3, s=1, p=1`:
$$
W_{out} = \lfloor \frac{(32 + 2 - 3)}{1} \rfloor + 1 = 32
$$
**Same size**. This is why `p = (k−1)/2 = 1` is the standard for 3×3.

### Worked example 2: strided conv

Input `32×32`, `Conv3×3, s=2, p=1`:
$$
W_{out} = \lfloor \frac{(32 + 2 - 3)}{2} \rfloor + 1 = 16
$$
**Halved.**

### Worked example 3: dilated conv

Input `32×32`, `Conv3×3, s=1, p=2, d=2`:
$$
k_{eff} = (3-1) \cdot 2 + 1 = 5
$$
$$
W_{out} = \lfloor \frac{(32 + 4 - 5)}{1} \rfloor + 1 = 32
$$
Same size. Note `p = 2` (not 1), because dilation increases the effective kernel.


# Trainable Parameter Count

## Conv Layer

For Conv2d(in_channels=**C_in**, out_channels=**C_out**, kernel_size=**k**)
$$
params = (C_{in} \cdot k \cdot k + 1) \cdot C_{out}
$$
Where:
- $C_{in} \cdot k \cdot k$ = weights per output channel (one filter)
- +1 = bias per output channel
- $\cdot C_{out}$ = one filter per output channel

> [!important] WATCH OUT
> If `bias=False`, drop the `+1`


## Fully Connected Layer
For Linear(in_features=**F_in**, out_features=**F_out**)

$$
params = (F_{in} + 1) \cdot F_{out}
$$

## Batch Norm
For BatchNorm2d(num_features=**C**) with `affine=True`

Trainable: **2C**, If `affine=False`, 0 trainable

## Worked examples

### Example 1: single conv

`Conv2d(3, 64, kernel_size=3, padding=1, bias=True)`

- Weights: `3 · 3 · 3 · 64 = 1728`
- Bias: `64`
- Total: `1792`

If `bias=False`: `1728`.


### Example 2: conv with 1×1 kernel

`Conv2d(256, 128, kernel_size=1)`

- Weights: `256 · 1 · 1 · 128 = 32768`
- Bias: `128`
- Total: `32896`

1×1 convs are cheap per pixel but can still have many parameters because `C_in · C_out` dominates.
### Example 3: Full Small CNN
```python
model = nn.Sequential(
    nn.Conv2d(3, 32, 3, padding=1),      # params: (3·9+1)·32 = 896
    nn.ReLU(),
    nn.Conv2d(32, 64, 3, padding=1),     # params: (32·9+1)·64 = 18496
    nn.ReLU(),
    nn.MaxPool2d(2),                     # 0 params
    nn.Conv2d(64, 128, 3, padding=1),    # params: (64·9+1)·128 = 73856
    nn.ReLU(),
    nn.AdaptiveAvgPool2d(1),             # 0 params
    nn.Flatten(),
    nn.Linear(128, 10),                  # params: (128+1)·10 = 1290
)
```

Let's compute each:

- Conv1: `(3·3·3 + 1) · 32 = (27+1)·32 = 896`
- Conv2: `(32·3·3 + 1) · 64 = (288+1)·64 = 18496`
- Conv3: `(64·3·3 + 1) · 128 = (576+1)·128 = 73856`
- FC: `(128+1) · 10 = 1290`

Total: `896 + 18496 + 73856 + 1290 = 94538` trainable parameters.


- **Q5.** A network has `Conv2d(3, 16, 3, padding=1) → ReLU → MaxPool2d(2) → Conv2d(16, 32, 3, padding=1) → ReLU → MaxPool2d(2) → Flatten → Linear(?, 10)`. Input `(1, 3, 32, 32)`. What is the `in_features` of the Linear layer? Total trainable params?

> [!answer]-
> **A5.**
> - Conv1 output: `(1, 16, 32, 32)`, params `(3·9+1)·16 = 448` 
> - MaxPool2 output: `(1, 16, 16, 16)` 
> - Conv2 output: `(1, 32, 16, 16)`, params `(16·9+1)·32 = 4640` 
> - MaxPool2 output: `(1, 32, 8, 8)` 
> - Flatten: `32 · 8 · 8 = 2048` 
> - Linear in_features = **2048**, params `(2048+1)·10 = 20490` 
> Total = `448 + 4640 + 20490 = 25578` trainable params.







