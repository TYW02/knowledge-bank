
# What it does

> [!important] What it does
> Optimization algorithm that **iteratively adjusts parameters** to **minimize a loss function**.
> - The core idea:
> 	- Compute **gradient of loss** with **respect to each parameter**, then take **a step** in the **opposite direction** of the gradient (Gradient points uphill, and we want to go downhill)

## Update Rule (Vanilla Gradient Descent)
$$
\theta_{t+1} = \theta_{t} - \eta \triangledown_{\theta}L(\theta_{t})
$$
Where:
- $\theta$ = parameters (weights, bias)
- $\eta$ = learning rate
- $\triangledown_{t} L$ = Gradient of loss with respect to the parameters
- $t$ = Current step

# Key Characteristics

| Characteristics         | Description                                                                         |
| ----------------------- | ----------------------------------------------------------------------------------- |
| First-order             | Uses only first derivatives (gradients), not curvature                              |
| Iterative               | Takes **many small steps**, not a closed-form solution                              |
| Local                   | Follows the local slope; **can get stuck** in **local minima** or **saddle points** |
| Learning rate sensitive | The single **most important** hyperparameter                                        |
| Scales with data        | Full-batch GD is **expensive**; **SGD** and mini-batch are **approximations**       |
| Guaranteed convergence  | For **convex losses** with a suitable learning rate, converges to global minimum    |

# Variants by how much data is used per step

## Batch Gradient Descent (BGD)
Compute gradients over the **entire** training set before each update
```python
for epoch in range(epochs):
    grad = compute_grad_over_all_data(params, X, y)
    params -= lr * grad
```

> [!success] PROS
> - Stable
> - Exact Gradient
> - Guaranteed descent for small enough $\eta$

> [!failure] CONS
> - Very slow per step
> - Memory-heavy
> - No stochasticity to escape bad regions
## Stochastic Gradient Descent (SGD)
Updates using 1 sample at a time
```python
for epoch in range(epochs):
    for i in range(len(X)):
        grad = compute_grad(params, X[i], y[i])
        params -= lr * grad
```

> [!success] PROS
> - Fast per step
> - Noise helps escape saddle points
> - Works online

> [!failure] CONS
> - Very noise update
> - Doesn't settle cleanly at the minimum

## Mini-batch Gradient Descent
The default in practice. Updates using a small batch (e.g. 32, 64, 128)
```python
for epoch in range(epochs):
    for xb, yb in dataloader:   # batch_size=64
        grad = compute_grad(params, xb, yb)
        params -= lr * grad
```

> [!success] PROS
> - Good balance of speed and stability
> - Leverages GPU parallelism

> [!failure] CONS
> - Introduces a batch-size hyperparameter


# How to calculate it

### Example 1: One parameter, manual

Minimize `L(w) = w²` starting at `w = 4`, learning rate `η = 0.1`.

- Gradient: `dL/dw = 2w`

| Step | `w`   | `dL/dw = 2w` | Update: `w ← w - 0.1 · 2w` |
| ---- | ----- | ------------ | -------------------------- |
| 0    | 4.00  | 8.00         | 4.00 − 0.80 = 3.20         |
| 1    | 3.20  | 6.40         | 3.20 − 0.64 = 2.56         |
| 2    | 2.56  | 5.12         | 2.56 − 0.512 = 2.048       |
| 3    | 2.048 | 4.096        | 2.048 − 0.410 = 1.638      |
| 4    | 1.638 | 3.277        | 1.638 − 0.328 = 1.310      |

Converging toward `w = 0` (the true minimum). The steps shrink because the gradient shrinks near the minimum.

### Example 2: Two parameters, manual

Minimize `L(w, b) = (w·x + b − y)²` with `x = 2`, `y = 5`.
- Start `w = 1`, `b = 0`, `η = 0.01`.
- Prediction: `ŷ = 1·2 + 0 = 2`.
- Error: `ŷ − y = 2 − 5 = −3`.
- Loss: `L = (−3)² = 9`.

Gradients (chain rule):
$$
\frac{\delta L}{\delta w} = 2(\hat{y} - y) \cdot x = 2(-3)(2) = -12
$$
$$
\frac{\delta L}{\delta b} = 2(\hat{y} - y) \cdot 1 = 2(-3) = -6
$$
Updates:
$$
w = 1 - 0.01 \cdot (-12) = 1 + 0.12 = 1.12
$$
$$
b = 0 - 0.01 \cdot (-6) = 0 + 0.06 = 0.06
$$
> [!important] New prediction: 
> `1.12·2 + 0.06 = 2.30`. Closer to 5. Loss dropped from 9 to `(2.30 − 5)² = 7.29`.


# PyTorch
```python
import torch

w = torch.tensor([1.0], requires_grad=True)
b = torch.tensor([0.0], requires_grad=True)
lr = 0.01

x = torch.tensor([2.0])
y = torch.tensor([5.0])

for step in range(100):
    y_pred = w * x + b
    loss = (y_pred - y) ** 2

    loss.backward()              # compute gradients

    with torch.no_grad():
        w -= lr * w.grad
        b -= lr * b.grad

    w.grad.zero_()               # clear for next step
    b.grad.zero_()

print(w.item(), b.item())        # ~2.5, ~0.0
```


## What happens when key parts change

### Learning rate `η`

| `η` too small             | `η` just right              | `η` too large                       |
| ------------------------- | --------------------------- | ----------------------------------- |
| Very slow convergence     | Smooth, steady descent      | Overshoots, oscillates, may diverge |
| Many iterations needed    | Reaches minimum efficiently | Loss may increase or become NaN     |
| May stall in flat regions |                             | Jumps out of good regions           |

> [!warning] **Too large example:** 
> - `L(w) = w²`, `w = 1`, `η = 1.1`.  
> Update: `w ← 1 − 1.1·2 = −1.2`. Next: `w ← −1.2 − 1.1·(−2.4) = 1.44`. **Oscillating** and growing → **diverges**.

> [!important] **Too small example:**
> `η = 0.0001`, same problem. `w = 1 → 0.9998 → 0.9996 → ...` takes **thousands of steps.**

### Batch size

| Small batch                           | Large batch                  |
| ------------------------------------- | ---------------------------- |
| Noisy gradients                       | Smooth gradients             |
| Can escape saddle points              | More stable but may stall    |
| Faster per step, more steps per epoch | Slower per step, fewer steps |
| Regularization effect                 | May need more epochs         |
| Lower memory                          | Higher memory                |
Rule of thumb: if you **scale batch size** by `k`, **scale learning rate** by roughly `k` (linear scaling rule) or `√k` (sqrt scaling rule) to keep training dynamics similar.






















































