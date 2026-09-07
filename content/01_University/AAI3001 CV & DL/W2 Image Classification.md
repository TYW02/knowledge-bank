---
title: W2 Image Classification
tags:
  - Classification
---
# Sigmoid
$\frac{1}{1 + e^{-f(x)}}$
- Maps any input value into a smooth S-shaped range between \[0, 1]
- Binary Classification: Used in final output layer or in Logistic Regression when outcome must be classified into 1 of 2 groups \[yes / no]
- DOES NOT SUM TO 1
- Can be interpreted as Probabilities

![[Pasted image 20260907220632.png]]

> [!Vanishing Gradient]
> Gradient vanishes for large positives and negative arguments $x$ 
> $\frac{dg(x)}{dx} = \frac{e^{-x}}{(1 + e^{-x})^{2}} = (1 - \frac{1}{1 + e^{-x}})(\frac{1}{1 + e^{-x}})$


# Softmax
$\frac{1}{1 + e^{-f(x^{n})}}$
- Returns **logits**, a set of probabilities that add up to **1**
- Multi-Class Classification: Since each, class's probability has to add up to 1 


# Rectified Linear Unit (ReLU)
- Fast to compute
- Gradients do not saturate (Grad does not flatten or shrink towards 0 as input grows larger)
- Not differentiable in 0
	- Not practical concern
	- Could define it to be 1
- Inactive neurons can act as implicit regularization
![[Pasted image 20260907221026.png]]

> [!Problems with ReLU]
> - Gradient is 0 for negative inputs
> - Might cause weight updates where grad become 0 and neuron will not activate again on any data.

# Leaky ReLU
```python
def leaky_relu(x, alpha=0.01):
	return max(x, alpha * x)
```

![[Pasted image 20260907221333.png]]
## Binary Cross-Entropy Loss (BCE)
$L = \sum_{n=1}^{N} -y^{n}ln(\hat{y}^{n} - (1 - y^{n})ln(1-\hat{y^{n}})$

![[Pasted image 20260907214907.png]]

> [!How to read this]
> $-1 * log(0.88) - 0 * log(0.12) = 0.1844$
> You can just read this as 
> $-1 * log(0.88)$
> Since the 2nd class `0` * by anything is still 0

![[Pasted image 20260907215131.png]]

> [!Meaning]
> Same here, since the logits are far from the expected / desired output, means we are making a bad prediction.
> Hence when we calculate BCE loss $-1 * log (0.12) = 3.035$ is high


![[Pasted image 20260907215345.png]]

![[Pasted image 20260907215358.png]]

> [!Summary]
> Basically Multi-Class means there are multiple possible classes but only **ONE** prediction.
> While Multi-Label means there are multiple possible classes and **Multiple** predictions

![[Pasted image 20260907220204.png]]

![[Pasted image 20260907221346.png]]

# Activation Function
- Introduces non-linearity: Learn complex data representations
- Should be **differentiable** if we are using gradient-based optimization
	- Differentiable meaning the function should have a flat gradient somewhere
- Proper selection of activation functions is important for training stable and effective models


# Neural Networks

> [!Definition: Neural Network]
> Any directed graph built from neurons is a neural network.

## 2 important types
- Feedforward NN: Simplest neural network, where neurons are in layers and 1 layer is fully connected to the next
- Recurrent NN for sequence processing

# Gradient Descent 
> [!Gradient Descent]
> Given: Learning rate $\eta$ initialize start vector to a value
> Run while loop, until function value changes very little:
> - $weight_{new}$ = $weight_{old} - \eta * \delta \frac{dL}{dw}$

- Minimizing gradient on training data ensures low loss on training data
- Does not guarantee low losses on new unseen test data

# Forward Propagation & Backpropagation
- Forward Propagation (Forward pass) refers to calculation and storage of intermediate variables (including outputs) for a neural network in order from the input layer to output layer
- Backpropagation refers to the method of calculating the gradient of neural network parameters
- Computation Graph: Represents the process of computing a mathematical expression in which we break down the computation into separate operations, each of which is modelled as a node in a graph.

![[Pasted image 20260907224844.png]]

> [!Note]
> This is basically what AutoGrad looks like


# Chain Rule
![[Pasted image 20260907225000.png]]


# Gradient in PyTorch - AutoGrad
![[Pasted image 20260907225025.png]]











































