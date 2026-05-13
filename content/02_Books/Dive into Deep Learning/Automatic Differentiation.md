#AutoGrad #Backpropagation

all modern deep learning frameworks take this work off our plates by offering _automatic differentiation_ (often shortened to _autograd_). As we pass data through each successive function, the framework builds a _computational graph_ that tracks how each value depends on others. 

To calculate derivatives, automatic differentiation works **backwards** through this graph applying the chain rule. The computational algorithm for applying the chain rule in this fashion is called _backpropagation_.


# A Simple Function

Let’s assume that we are interested in differentiating the function $y = 2x^T x$ with respect to the column vector $x$. To start, we assign `x` an initial value.
```python
x = torch.arange(4.0)
x
# tensor([0., 1., 2., 3.])
```

Before we calculate the gradient of $y$ with respect to $x$, we need a place to store it. In general, we avoid allocating new memory every time we take a derivative because deep learning requires successively computing derivatives with respect to the same parameters a great many times, and we might risk running out of memory. Note that the gradient of a scalar-valued function with respect to a vector $x$ is vector-valued with the same shape as $x$.
```python
# Can also create x = torch.arange(4.0, requires_grad=True)
x.requires_grad_(True)
x.grad  # The gradient is None by default
```

We now calculate our function of $x$ and assign the result to $y$
```python
y = 2 * torch.dot(x, x)
y
# tensor(28., grad_fn=<MulBackward0>)
```

We can now take the gradient of $y$ with respect to $x$ by calling its backward method. Next, we can access the gradient via x's grad attribute
```python
y.backward()
x.grad
# tensor([ 0.,  4.,  8., 12.])
```

We already know that the gradient of the function $y = 2x^Tx$ with respect to $x$ should be $4x$. We can now verify that the automatic gradient computation and the expected result are identical.
```python
x.grad == 4 *x
# tensor([True, True, True, True])
```

Now let’s calculate another function of `x` and take its gradient. Note that PyTorch does not automatically reset the gradient buffer when we record a new gradient. Instead, the new gradient is added to the already-stored gradient. This behavior comes in handy when we want to optimize the sum of multiple objective functions. To reset the gradient buffer, we can call `x.grad.zero_()` as follows:
```python
x.grad.zero_()  # Reset the gradient
y = x.sum()
y.backward()
x.grad
# tensor([1., 1., 1., 1.])
```


# Backward for Non-Scalar Variables

Because deep learning frameworks vary in how they interpret gradients of non-scalar tensors, PyTorch takes some steps to avoid confusion. Invoking `backward` on a non-scalar elicits an error unless we tell PyTorch how to reduce the object to a scalar. More formally, we need to provide some vector $v$ such that `backward` will compute $v^T\partial_xy$ rather than $\partial_xy$ . This next part may be confusing, but for reasons that will become clear later, this argument (representing $v$) is named `gradient`. For a more detailed description, see Yang Zhang’s [Medium post](https://zhang-yang.medium.com/the-gradient-argument-in-pytorchs-backward-function-explained-by-examples-68f266950c29).

```python
x.grad.zero_()
y = x * x
y.backward(gradient=torch.ones(len(y)))  # Faster: y.sum().backward()
x.grad
# tensor([0., 2., 4., 6.])
```


# Gradients and Python Control Flow

So far we reviewed cases where the path from input to output was well defined via a function such as `z = x * x * x`. Programming offers us a lot more freedom in how we compute results. For instance, we can make them depend on auxiliary variables or condition choices on intermediate results. One benefit of using automatic differentiation is that even if building the computational graph of a function required passing through a maze of Python control flow (e.g., conditionals, loops, and arbitrary function calls), we can still calculate the gradient of the resulting variable. To illustrate this, consider the following code snippet where the number of iterations of the `while` loop and the evaluation of the `if` statement both depend on the value of the input `a`.

```python
def f(a):
    b = a * 2
    while b.norm() < 1000:
        b = b * 2
    if b.sum() > 0:
        c = b
    else:
        c = 100 * b
    return c
```

Below, we call this function, passing in a random value, as input. Since the input is a random variable, we do not know what form the computational graph will take. However, whenever we execute `f(a)` on a specific input, we realize a specific computational graph and can subsequently run `backward`.

```python
a = torch.randn(size=(), requires_grad=True)
d = f(a)
d.backward()
```

Even though our function `f` is, for demonstration purposes, a bit contrived, its dependence on the input is quite simple: it is a _linear_ function of `a` with piecewise defined scale. As such, `f(a) / a` is a vector of constant entries and, moreover, `f(a) / a` needs to match the gradient of `f(a)` with respect to `a`.
```python
a.grad == d / a
# tensor(True)
```

Dynamic control flow is very common in deep learning. For instance, when processing text, the computational graph depends on the length of the input. In these cases, automatic differentiation becomes vital for statistical modeling since it is impossible to compute the gradient _a priori_.

















