

This limiting procedure is at the root of both _differential calculus_ and _integral calculus_. The former can tell us how to increase or decrease a function’s value by manipulating its arguments. 

This comes in handy for the _optimization problems_ that we face in deep learning where we repeatedly update our parameters in order to decrease the loss function.

Optimization addresses how to fit our models to training data, and calculus is its key prerequisite. However, do not forget that our ultimate goal is to perform well on _previously unseen_ data. That problem is called _generalization_ and will be a key focus of other chapters.


```python
%matplotlib inline
import numpy as np
from matplotlib_inline import backend_inline
from d2l import torch as d2l
```



# Derivatives and Differentiation

### What is a Derivative ?
- A Derivative is the _rate of change in a function_ with respect to **changes** in its arguments
	- How much does something change when I move its arguments

Derivatives can tell us how rapidly a loss function would increase or decrease if we were to _increase_ to _decrease_ each parameter by an infinitely small amount.

For functions $f: R -> r$ that map from scalars to scalars, the derivative of $f$ at a point $x$ is defined as

$f(x) = \lim_{h\to0} \frac{f(x + h) - f(x)}{h}$


This term on the right hand side is called a _limit_ and it tells us what happens to the value of an expression as a specified variable approaches a particular value.
- What happens to this expression as h approaches 0

This limit tells us what the ratio between a perturbation $h$ and the change in the function value $f(x+h)-f(x)$ converges to as we shrink its size to zero.


We can interpret the derivative $f'(x)$ as the _instantaneous_ rate of change of $f(x)$ with respect to $x$. Let’s develop some intuition with an example. Define $u = f(x)=3x^2-4x$.
```python
def f(x):
	return 3 * x ** 2 - 4 * x
```


---
Setting $x = 1$, we see that $\frac{f(x+h)-f(x)}{h}$ approaches 2 as $h$ approaches 0. While this experiment lacks the rigor of a mathematical proof, we can quickly see that indeed $f'(1)=2$.

```python
for h in 10.0**np.arange(-1, -6, -1):
	print(f'h={h:.5f}, numerical limit={(f(1+h)-f(1))/h:.5f}')
	
# h=0.10000, numerical limit=2.30000
# h=0.01000, numerical limit=2.03000
# h=0.00100, numerical limit=2.00300
# h=0.00010, numerical limit=2.00030
# h=0.00001, numerical limit=2.00003
```

![[Pasted image 20250825190547.png]]


# Visualization Utilities

We can visualize the slopes of functions using the `matplotlib` library. We need to define a few functions. As its name indicates, `use_svg_display` tells `matplotlib` to output graphics in SVG format for crisper images. The comment `#@save` is a special modifier that allows us to save any function, class, or other code block to the `d2l` package so that we can invoke it later without repeating the code, e.g., via `d2l.use_svg_display()`.
```python
def use_svg_display():  #@save
    """Use the svg format to display a plot in Jupyter."""
    backend_inline.set_matplotlib_formats('svg')
```

Conveniently, we can set figure sizes with `set_figsize`. Since the import statement `from matplotlib import pyplot as plt` was marked via `#@save` in the `d2l` package, we can call `d2l.plt`.
```python
def set_figsize(figsize=(3.5, 2.5)):  #@save
    """Set the figure size for matplotlib."""
    use_svg_display()
    d2l.plt.rcParams['figure.figsize'] = figsize
```

The `set_axes` function can associate axes with properties, including labels, ranges, and scales.
```python
#@save
def set_axes(axes, xlabel, ylabel, xlim, ylim, xscale, yscale, legend):
    """Set the axes for matplotlib."""
    axes.set_xlabel(xlabel), axes.set_ylabel(ylabel)
    axes.set_xscale(xscale), axes.set_yscale(yscale)
    axes.set_xlim(xlim),     axes.set_ylim(ylim)
    if legend:
        axes.legend(legend)
    axes.grid()
```

With these three functions, we can define a `plot` function to overlay multiple curves. Much of the code here is just ensuring that the sizes and shapes of inputs match.
```python
#@save
def plot(X, Y=None, xlabel=None, ylabel=None, legend=[], xlim=None,
         ylim=None, xscale='linear', yscale='linear',
         fmts=('-', 'm--', 'g-.', 'r:'), figsize=(3.5, 2.5), axes=None):
    """Plot data points."""

    def has_one_axis(X):  # True if X (tensor or list) has 1 axis
        return (hasattr(X, "ndim") and X.ndim == 1 or isinstance(X, list)
                and not hasattr(X[0], "__len__"))

    if has_one_axis(X): X = [X]
    if Y is None:
        X, Y = [[]] * len(X), X
    elif has_one_axis(Y):
        Y = [Y]
    if len(X) != len(Y):
        X = X * len(Y)

    set_figsize(figsize)
    if axes is None:
        axes = d2l.plt.gca()
    axes.cla()
    for x, y, fmt in zip(X, Y, fmts):
        axes.plot(x,y,fmt) if len(x) else axes.plot(y,fmt)
    set_axes(axes, xlabel, ylabel, xlim, ylim, xscale, yscale, legend)
```

Now we can plot the function $u = f(x)$ and its tangent line $y = 2x -3$ at $x = 1$ , where the coefficient is the slope of the tangent line.
```python
x = np.arange(0, 3, 0.1)
plot(x, [f(x), 2 * x - 3], 'x', 'f(x)', legend=['f(x)', 'Tangent line (x=1)'])
```

![../_images/output_calculus_7e7694_56_0.svg](https://d2l.ai/_images/output_calculus_7e7694_56_0.svg)


# Partial Derivatives and Gradients

Thus far, we have been differentiating functions of just one variable. In deep learning, we also need to work with functions of _many_ variables. We briefly introduce notions of the derivative that apply to such _multivariate_ functions.

Let $y = f(x_1, x_2,...x_n)$ be a function with $n$ variables. The partial derivative of $y$ with respect to its $i^{th}$ parameter $x_i$ is :
![[Pasted image 20250825191425.png]]


# Chain Rule

In deep learning, the gradients of concern are often difficult to calculate because we are working with deeply nested functions (of functions (of functions...)). Fortunately, the chain rule takes care of this. 
Returning to functions of a single variable, suppose that $y = f(g(x))$ and that the underlying functions $y = f(u)$ and $u =g(x)$ are both differentiable. The chain rule states that
$\frac{dy}{dx} = \frac{dy}{du}\frac{du}{dx}$

Turning back to multivariable functions, suppose that $y = f(u)$ has variables $u_1,u_2,...u_m$ where each $u_i = g_i(x)$ has variables $x_1,x_2,...x_n$ i.e. $u = g(x)$ Then the chain rule states that.
![[Pasted image 20250825191900.png]]
Where $A \in R^{nxm}$ is a _matrix_ that contains the derivative of vector $u$ with respect to vector $x$.
Thus, evaluating the gradient requires computing a vector-matrix product. This is one of the key reasons why linear algebra is such an integral building block in building deep learning systems.

































