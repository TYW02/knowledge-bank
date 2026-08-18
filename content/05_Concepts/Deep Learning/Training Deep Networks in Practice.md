---
title: Training Deep Networks in Practice
tags:
  - Optimizer
---
# Epochs, Batches, Iterations
Epochs: 1 Complete pass through the entire training dataset
Batch: Small subset of training data used for 1 forward and backward pass
Iterations: 1 weight update. 
	If you have 1000 training examples and batch size = 100:
	1000/100 = 10 Iterations per epoch


# Optimizers

Basic Update: $w_{new} = w_{old} - \eta \frac{dL}{dw}$
In practice, vanilla SGD can be slow and noisy, several optimizers improve on it.

## Momentum
Helps optimizer build speed in directions where the gradient consistently points the same way.

Momentum Update: $v = \beta v - \eta \frac{dL}{dw}$
$w = w + v$

Where $\beta$ controls how much past velocity is retained (often 0.9)
If gradient keeps pointing the same direction, velocity accumulates and the update becomes larger.
If the gradient changes direction often, velocity helps cancel out oscillations.

## Adam
Adam combines 2 ideas:
1. Momentum: Smooths gradient over time
2. Adaptive learning rates: Gives each parameter its own learning rate based on how frequently it changes.

If a weight's gradient has been consistently large, Adam reduces its effective learning rate
If a weight's gradient has been consistently small, Adam increases its effective learning rate

# Regularization
A model that is too flexible can memorize the training data.
Regularization reduces overfitting

## L2 Regularization / Weight Decay
Add a penalty to the loss based on the size of the weights:
$L_{total} = L_{original} + \frac{\lambda}{2}\sum_{i}{w^{2}_{i}}$

Where $\lambda$ controls the penalty strength.

Intuition:
Large weights often mean the model is fitting very sharp patterns in the training data. By keeping weights small, the model is forced to learn smoother, more general patterns.

In PyTorch this is **weight decay** and is set directly in the optimizer.


## Dropout
Dropout randomly turns off a fraction of neurons in a layer.

If dropout probability $p = 0.5$ means each neuron has a 50% chance of being temporarily removed during 1 training step.

> [!Why does this help?]
The network cannot rely on any single neuron because that neuron might be dropped. It must learn redundant, robust representations.
At **test time**, dropout is turned off, and the full network is used.


> [!In PyTorch]
> ```python
> import torch.nn as nn
> model = nn.Sequential(
> 	nn.Linear(784, 256),
> 	nn.ReLU(),
> 	nn.Dropout(0.5),
> 	nn.Linear(256, 10)
> )
> ```


## Early Stopping
During training we monitor both training loss and validation loss.

Typically:
- Training loss keeps decreasing
- Validation loss decreases for a while, then starts increasing

The point where validation loss starts increasing is where the model begins to overfit.
Early stopping means we stop training when validation loss has not improved for a number of epochs.




















