---
title: Hidden Layer
---
![[four_nodes.png]]


We are given an input node of 3 here so we have
```python
input = [2, 1, 3]
```

# How to calculate hidden layer
We will take the $\sum (weights * input ) + bias$

So for instance we see hidden node `a` it has the randomized weight and bias:
```python
a = [1, -1, -1, -5]
```

### Calculation
$a = 2(1) + 1(-1) + 3(-1) -5$

So here we get -1

Then we run through [ReLU](https://www.geeksforgeeks.org/deep-learning/relu-activation-function-in-deep-learning/) and get the final value of `0`.

> [!NOTE]
> Take note here that in the image, I did not draw the lines for weights of 0 since they aren't activated anyways.
> 
> After the calculation and ReLU of all 4 nodes we can then pass it onto other layers OR pass it to an output layer.




