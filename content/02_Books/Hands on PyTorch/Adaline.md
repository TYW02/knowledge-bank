---
title: Adaline
---
Uses Identity function instead of step function in Perceptron

This changes how the model converges. In perceptron the model will not converge and will just keep changing till it runs out of epochs.

But if Adaline that uses Identity function which is differentiable, the model can converge to the best estimate even if the classes are not linearly separable.


## What does Gradient based on whole training dataset mean ?
Every learning algorithm does the same thing: Minimize a loss function by adjusting weights in the direction that reduces error.

The main question is "error measured on how much data, before you take a step ?"

2 Extremes:
- 1 example at a time: Compute error for 1 example, immediately nudge weight, move to next sample. This is what [[Perceptron]] does.
- Entire dataset at once: Run every single example through the model collect *all* the errors, average them into 1 single gradient, and take 1 step. This is [[Adaline]] also called [batch gradient descent](https://www.geeksforgeeks.org/machine-learning/difference-between-batch-gradient-descent-and-stochastic-gradient-descent/).

## Explaining the code
```python
sekf.w_ += self.eta * 2.0 * X.T.dot(errors) / X.shape[0]
```

Here the Loss function we are using is MSE which is $(1/n) \sum(y_i - output_i)^2$

### Deriving the loss function
${\partial Loss} / {\partial W} = (1/n) \sum2(y_i - output_i)(-X_i)$
$=  -(2/n) * X^T * (y - output)$

Gradient Step = $w = w - \alpha * {\partial Loss}$
$= w + \alpha * (2/n) * X^T * errors$

That is exactly what `X.T.dot(errors)` is doing it sums up `error_i * x_i` across all rows which is the whole dataset

## What is `X.T.dot(errors)`
> [!Test Yourself]-
> It computes the sum over all `n` training examples.









