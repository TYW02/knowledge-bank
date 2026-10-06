
# Definition
$$
\frac{1}{1 + e^{-f(x)}}
$$
- Maps any input value into a smooth S-shaped range between \[0, 1]
- Binary Classification: Used in final output layer or in Logistic Regression when outcome must be classified into 1 of 2 groups \[yes / no]
- **DOES NOT SUM TO 1**
- Can be interpreted as Probabilities

> [!important] Main Idea: What it does
> The sigmoid function **squashes** any real-values input **into the range** (0, 1).
> - It's an S-shaped curve 


# Derivative
$$
\sigma(x) \cdot (1 - \sigma(x))
$$


## How to Derive
![[Sigmoid Derivation.svg]]


### Example
- g(0) = 0.5

> Derivative of sigmoid is g(x)(1 - g(x))
> 
> 0.5 * (1 - 0.5) = 0.25


# Key Properties

| Property            | Value                               |
| ------------------- | ----------------------------------- |
| Output Range        | `(0, 1)` - **NEVER** exactly 0 or 1 |
| At `x = 0`          | $\sigma(0) = 0.5$                   |
| As $x$ -> $+\infty$ | $\sigma(x)$ -> $1$                  |
| As $x$ -> $-\infty$ | $\sigma(x)$ -> $0$                  |
| Monotonic           | Yes, strictly increasing            |
| Symmetry            | $\sigma(-x) = 1 - \sigma(x)$        |
| Derivative Max      | `0.25` at `x = 0`                   |

# What it's used for

## 1. Binary classification output layer
Produces a **probability** for the **positive class**. Often paired with `BCELoss` or `BCEWithLogitsLoss`
## 2. Gates in LSTMs and GRUs
- Forget, input, output Gate all use sigmoid to **produce values (0, 1)** that control how much information passes through
## 3. Multi-label Classification
- Each output neuron **independently uses sigmoid**, unlike softmax which forces output to sum to 1.

# PyTorch code Examples

## Basic Usage
```python
import torch
import torch.nn as nn

x = torch.tensor([-3.0, -1.0, 0.0, 1.0, 3.0])
y = torch.sigmoid(x)
print(y)
# tensor([0.0474, 0.2689, 0.5000, 0.7311, 0.9526])
```
## As a module
```python
m = nn.Sigmoid()
out = m(torch.tensor([-2.0, 0.0, 2.0]))
# tensor([0.1192, 0.5000, 0.8808])
```
## In a binary classifier
```python
class BinaryClassifier(nn.Module):
    def __init__(self, in_features):
        super().__init__()
        self.fc1 = nn.Linear(in_features, 16)
        self.fc2 = nn.Linear(16, 1)

    def forward(self, x):
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return torch.sigmoid(x)   # probability in (0, 1)
```
## With Loss Function
```python
# Option A: sigmoid + BCELoss
model = BinaryClassifier(10)
pred = model(x)                    # already sigmoid-ed
loss = nn.BCELoss()(pred, target)

# Option B: raw logits + BCEWithLogitsLoss (more numerically stable)
class BinaryClassifierLogits(nn.Module):
    def forward(self, x):
        return self.fc2(torch.relu(self.fc1(x)))  # no sigmoid

logits = model(x)
loss = nn.BCEWithLogitsLoss()(logits, target)
```

 > `BCEWithLogitsLoss` applies **sigmoid internally** and is **preferred** because it **avoid numerical issues** when the logits is very large or very small


# Worked Example

## Example 1: 
$$
\sigma(0) = \frac{1}{1+e^{-0}} = \frac{1}{1 + 1} = \frac{1}{2} =0.5
$$
## Example  2:
$$
e^{2} = 7.3891
$$
$$
\sigma(-2) = \frac{1}{1+7.3891} = \frac{1}{8.3891} = 0.1192
$$
- Notice: $\sigma(-2) = 1 - \sigma(2) = 1 - 0.8808 = 0.1192$

## Example 3: (With Derivative)
$$
e^{-5} = 0.006738
$$
$$
\sigma(5) = \frac{1}{1+0.006738} = 0.9933
$$
Derivative:
$\sigma'(5) = 0.9933 * (1 - 0.9933) = 0.9933 * 0.0067 = 0.00665$


### Example 6: Binary classification interpretation
Suppose a model outputs logit `z = 1.5`. The predicted probability of the positive class is:
$$
\sigma(1.5) = \frac{1}{1+e^{-1.5}} = \frac{1}{1+0.2231} = 0.8176
$$
So the model thinks there's **about an 82% chance** the sample belongs to class 1.
If the true label is 1, the binary cross-entropy loss is:
$$
L = -log(0.8176) = 0.2013
$$
If the true label is 0:
$$
L = -log(1 - 0.8176) = -log(0.1824) = 1.7014
$$


# Summary
- Maps any real number to `(0, 1)` using `1 / (1 + e^{-x})`
- **Standard choice** for **binary classification outputs** and for gates in recurrent architectures
- Derivative is $\sigma(x)(1-\sigma(x))$, maxing out at 0.25.
- Because it **saturates** and **kills gradients for large** `|x|`, it's **rarely used** in **hidden layers** of modern deep networks














































