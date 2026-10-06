# Softmax
- Returns **logits**, a set of probabilities that add up to **1**
- **Multi-Class** Classification: Since each, class's probability has to add up to 1 

> [!important] What it does
> Softmax takes a vector of real-valued **logits** and converts it into a probability distribution every output is in `(0, 1)` and they **all sum to 1**

Key Idea: **Exponentiate each element**, then **divide by the sum**.
- **Larger logits** get **exponentially more weight**, so **softmax** is "**winner-takes-more**" but **still smooth**
## Formula

> [!important] Formula for Single Softmax
> $$
> \frac{e^{z_{i}}}{\sum^{K}_{j=1}{e^{z_{j}}}}
> $$
- When we take the **Sum of Softmax** we take the Sum of **ALL the softmax calculation** we have done.

> [!important] This is what is looks like
> $$
> \sum\frac{e^{i}}{\sum{e^{j}}}
> $$
> We can move the **Sum** up to the **numerator** and **evaluates to the same** as the **denominator**.
> - This means that we are essentially taking the **same number divided by itself**.
> - Hence we get **1.**

# Key Properties
| Property        | Value                                             |
| --------------- | ------------------------------------------------- |
| Output Range    | Each value in `(0, 1)`                            |
| Sum of outputs  | Exactly 1                                         |
| Preserves order | If $z_{i} > z_{j}$ then softmax(z)i > softmax(z)j |
| Shift invariant | softmax(z) = softmax(z + c) for any constant `c`  |
| Not elementwise | Depends on the whole vector, unlike sigmoid       |
| At equal logits | Uniform distribution `1/k` for each               |
The **shift invariance** matters a lot in practice: **Adding a constant** to every logit **doesn't change the output**. This is what **enables the numerically stable implementation** (Subtract the max)

# What it's used for

## 1. Multi-class classification output layer
- One class per output, exactly 1 correct answer.
- Usually paired with `CrossEntropyLoss` / `NLLLoss`
## 2. Attention Mechanisms
- Softmax over attention scores produces weights that sum to 1, used to take a weighted average of values
## 3. Reinforcement Learning
- Softmax over Q-values or action preferences to get a stochastic policy
## 4. Mixture models / routing
- Gating weights that sum to 1 (e.g. Mixture of Experts)
## 5. Knowledge Distilation
- With a temperature parameter, softmax produces "soft targets" from a teacher's logits

### Common Pattern
In PyTorch, `nn.CrossEntropyLoss` expects **raw logits** (no softmax), because it applies `log_softmax` internally for numerical stability. 

DO NOT apply softmax before `CrossEntropyLoss`


# PyTorch Code Examples

## Basic Usage
```python
import torch
import torch.nn as nn
import torch.nn.functional as F

z = torch.tensor([1.0, 2.0, 3.0])

print(torch.softmax(z, dim=0))
# tensor([0.0900, 0.2447, 0.6652])
# sum = 1.0
```

## As a module
```python
m = nn.Softmax(dim=1)   # dim is required for nn.Softmax
x = torch.tensor([[1.0, 2.0, 3.0],
                  [1.0, 1.0, 1.0]])
print(m(x))
# tensor([[0.0900, 0.2447, 0.6652],
#         [0.3333, 0.3333, 0.3333]])
```

## `dim` matters - Batch vs Classes
```python
x = torch.randn(4, 5)   # batch=4, classes=5

# Correct: normalize over classes
probs = torch.softmax(x, dim=1)   # rows sum to 1

# Wrong for classification: normalizes over the batch
wrong = torch.softmax(x, dim=0)   # columns sum to 1
```

> [!important] 
> Always think about **which dimension** you want to **sum to 1.**


## In a multi-class classifier
```python
class Classifier(nn.Module):
    def __init__(self, in_features, num_classes):
        super().__init__()
        self.fc1 = nn.Linear(in_features, 32)
        self.fc2 = nn.Linear(32, num_classes)

    def forward(self, x):
        x = torch.relu(self.fc1(x))
        return self.fc2(x)   # return raw logits
        
        
logits = model(x)

# Training (logits + CrossEntropyLoss)
loss = nn.CrossEntropyLoss()(logits, targets)

# Inference (get probabilities)
probs = torch.softmax(logits, dim=1)
preds = probs.argmax(dim=1)
```

### Log-Softmax (Numerically better)
```python
# These are mathematically equal, but log_softmax is more stable
log_probs = F.log_softmax(logits, dim=1)
# vs
log_probs2 = torch.log(torch.softmax(logits, dim=1))  # can underflow
```

Used with `nn.NLLLosee`
```python
loss = nn.NLLLoss()(F.log_softmax(logits, dim=1), targets)
```



## Worked examples

### Example 1: Simple 3-class vector

Compute `softmax([1, 2, 3])`.

**Step 1 — exponentiate:**
$e^{1} = 2.7183$
$e^2 = 7.3891$
$e^3 = 20.0855$

**Step 2 — sum:**
2.7183+7.3891+20.0855=30.19292

**Step 3 — divide each:**
$$
softmax(z)_{1} = \frac{2.7183}{30.1929} = 0.0900
$$

$$
softmax(z)_{2} = \frac{7.3891}{30.1929} = 0.2447
$$
$$
softmax(z)_{3} = \frac{20.0855}{30.1929} = 0.6652
$$

**Check:** `0.0900 + 0.2447 + 0.6652 ≈ 1.0000` 
Class 3 has the **highest logit** and gets the **highest probability**, but it's **not overwhelming** because the **logits are close.**


## Softmax vs sigmoid

|                           | Sigmoid<br>                    | Softmax<br>                      |
| ------------------------- | ------------------------------ | -------------------------------- |
| Input                     | Scalar (elementwise)           | Vector                           |
| Output sum                | Each in `(0,1)`, no constraint | Exactly 1                        |
| Use case                  | Binary / multi-label           | Multi-class (mutually exclusive) |
| Loss partner              | `BCEWithLogitsLoss`            | `CrossEntropyLoss`               |
| Depends on other outputs? | No                             | Yes                              |

**Rule of thumb:**
- Labels are **mutually exclusive** → softmax + cross-entropy.
- Labels are **independent** (multi-label) → sigmoid per class + binary cross-entropy.


## Common pitfalls

1. **Wrong `dim`.** In a `(batch, classes)` tensor, softmax over `dim=1`. Using `dim=0` **normalizes** across the **batch**, which is almost always wrong.
2. **Applying softmax before `CrossEntropyLoss`.** Double-softmaxing. Pass raw logits to `CrossEntropyLoss`; it handles softmax internally (via `log_softmax`).
3. **Numerical overflow.** Don't compute `e^z` naively for large `z`. Use `torch.softmax`, `F.log_softmax`, or subtract the max first.
4. **Treating softmax as independent per element.** It isn't — changing one logit changes all outputs.
5. **Using softmax for multi-label problems.** If a sample can belong to multiple classes simultaneously, use sigmoid per class instead.
6. **Forgetting it's temperature-scalable.** In distillation or calibrated inference, `T ≠ 1` often helps.

##### Summary
Softmax converts a **vector of logits** into a **probability distribution** using `e^{zᵢ} / Σ e^{zⱼ}`. 
- Outputs are in `(0, 1)` and **sum to 1**, which makes it the natural choice for **multi-class classification**, attention weights, and any place you need a normalized weighting over a set of options. 
- It's **shift-invariant**, so **subtracting the max** is a **free numerical stability** win that PyTorch does automatically. For **training** classifiers, use **raw logits** with `CrossEntropyLoss`; only apply softmax **explicitly** when you actually **need probabilities** at **inference or for downstream** use.






























