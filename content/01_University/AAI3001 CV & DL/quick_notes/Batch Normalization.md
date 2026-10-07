

# What it does

> [!important] Main Idea
> **Normalizes** the **activations** of a layer across the **batch dimension** ==🟢during training==. It **stabilizes and speeds** up training by keeping the **distribution of layer** inputs **roughly consistent** across iterations.

> [!success] Core Idea
> For **each feature** (Channel), compute the **mean and variance** over the **current mini-batch**, **normalize** to **zero mean** and **unit variance**, then apply a **learnable** scale `γ` and shift `β`


# The Formula
For a mini-batch `B = {X1, ...m x_m}` of activations at a given channel:

## Step 1: Batch Mean
$$
\mu_{B} = \frac{1}{m}\sum^{m}_{i=1} x_i
$$

## Step 2: Batch Variance
$$
\sigma^{2}_{B} = \frac{1}{m} \sum^{m}_{i=1}(x_i - \mu_{B})^2
$$

## Step 3: Normalize
$$
\hat x_{i} = \frac{x_{i} - \mu_{B}}{\sqrt{\sigma^{2}_{B} + \epsilon}}
$$
## Step 4: Scale and Shift
$$
y_i = \gamma \hat{x_i} + \beta
$$

Where:
- `m` = batch size (per channel)
- $\epsilon$ = small constant (default `1e-5`) for numerical stability
- $\gamma$ = learnable scale, one per channel
- $\beta$ = learnable shift, one per channel

$\gamma$ and $\beta$ let the network **undo** the normalization if that's optimal. Without them, BatchNorm would restrict the representational power of the layer

# Training vs Inference

> MOST IMPORTANT THING

## Training Mode (`model.train()`)
- Uses the current batch's mean and variance
- Updates `running_mean` and `running_var` with an exponential moving average


## Inference Model (`model.eval()`)
- Uses the stored `running_mean` and `running_var`
- Does **NOT** update them
- Normalizes using population statistics

> [!warning] Why the difference ?
> At **inference**, you might **process one sample at a time**, so there's **no batch to compute statistics** from.
> - The running statistics accumulated **during training** approximate the **population statistics**

## If you forget `.eval()`
- Dropout stays active (randomly zeroing activations)
- BatchNorm uses batch statistics of your validation set (which may be small or biased)
- Running stats get polluted with validation data
- Validation metrics become unreliable


# Shape and Parameter Count
For `BatchNorm2d(num_feature=C)`

|Component|Shape|Trainable?|
|---|---|---|
|`weight` (γ)|`(C,)`|Yes|
|`bias` (β)|`(C,)`|Yes|
|`running_mean`|`(C,)`|No (buffer)|
|`running_var`|`(C,)`|No (buffer)|
|`num_batches_tracked`|scalar|No (buffer)|
- Trainable params: `2C` (γ and β) if `affine=True`, else 0.    
- Buffers: `2C + 1` non-trainable.
**Normalization dimension for `(N, C, H, W)`:** mean and variance are computed over `N, H, W` for each channel `C`. So each channel gets its own mean and variance.
**For `(N, C, L)` (1D):** normalized over `N, L` per channel.
**For `(N, F)` (Linear input):** `BatchNorm1d(F)` normalizes over `N` per feature

# Why BatchNorm helps

## 1. Reduces internal covariate shift
Layer inputs stay in a stable range, later layers don't have to constantly adapt

## 2. Smooths the loss landscape
Smoother landscape (Larger learning rates are stable)

## 3. Allows higher learning rate
Without BatchNorm, high LR often diverges. With it, you can use 10x larger LR

## 4. Reduces sensitivity to initialization
Weight can be initialized less carefully

## 5. Acts as a regularizer
The batch statistics add noise, similar to dropout.
- This can reduce overfitting slightly

## 6. Speeds up convergence
- Fewer epochs to reach the same accuracy

## 7. Enables deeper networks
- ResNet-152 would be much harder to train without BatchNorm

# Effects on Gradients
- BatchNorm **changes gradient flow**. Gradients through BatchNorm **depend on the whole batch**
- The gradient w.r.t. `x_i` involves terms from all other samples in the batch. This couples samples together
- This is why BatchNorm **doesn't work well** with **very small batch sizes**

# Effects on Inference
- **Inference** uses **running stats**, which are **frozen**. So the **model is deterministic**
- If running stats are **poorly estimated** (short training, small batches), **inference performance suffers**
- Common Trick: Train with a **larger batch near the end** to get better running stats


## Worked Example
Batch of 4 samples, 1 channel, `2x2` feature map. $\epsilon = 0$
```text
Sample 1: [[1, 2],
           [3, 4]]
Sample 2: [[5, 6],
           [7, 8]]
Sample 3: [[9, 10],
           [11, 12]]
Sample 4: [[13, 14],
           [15, 16]]
```

Compute **mean** over all `4 x 4 = 16` values:
$$
\mu = \frac{1 + 2 + ... + 16}{16} = \frac{136}{16} = 8.5
$$
Compute **Variance**
$$
\sigma^{2} = \frac{1}{16}\sum(x_{i} - 8.5)^{2} = \frac{340}{16} = 21.25
$$
**Normalize** each value
$$
\hat x_{i} = \frac{x_{i} - 8.5}{\sqrt{21.25}} = \frac{x_{i}-8.5}{4.61}
$$
For x = 1: $(1 - 8.5) / 4.61 = -1.63$
For x= 16: $(16 - 8.5) / 4.61 =  +1.63$

**Apply** $\gamma$ and $\beta$ (say = $\gamma = 2$, $\beta = 1$)
$y_{1} = 2 \cdot (-1.63) + 1 = -2.26$
$y_{16} = 2 \cdot (1.63) + 1 = 4.26$


# Where to place BatchNorm
```python
nn.Conv2d(3, 64, 3, padding=1, bias=False),
nn.BatchNorm2d(64),
nn.ReLU(inplace=True),
```

- BN after conv, before activation
- This is the dominant convention in ResNet, EfficientNet, etc


# Summary
BatchNorm **normalizes** activations across the batch to **zero mean and unit variance**, then applies a learnable scale `γ` and shift `β`. 
- During **training** it uses **batch statistics** and **updates running estimates**
- During **inference** it uses the **stored running statistics.** 
- It **speeds up training**, allows **larger learning rates**, reduces initialization sensitivity, and acts as a mild regularizer. It works best with batch sizes ≥ 32
- Place it **after conv/linear layers** and **before activations**, drop the bias from the preceding layer, and always call `.eval()` during validation and inference.











































