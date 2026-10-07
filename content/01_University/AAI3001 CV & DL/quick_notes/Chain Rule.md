
# Fundamental Rules

## 1. Constant Rule
$$
\frac{d}{dx}[c] = 0
$$
A constant doesn't change when `x` changes, so its rate of change is zero.

> [!note] In Deep Learning
> Biases that aren't being differentiated, or terms treated as constants during partial differentiation


## 2. Constant Multiple Rule
$$
\frac{d}{dx}[c \cdot f(x)] = c \cdot f'(x)
$$
The constant just rides along

- Example: d/dx\[$5x^2$\] = $5 \cdot 2x = 10x$

## 3. Power Rule
$$
\frac{d}{dx}[x^{n}] = n \cdot x^{n-1}
$$
**Examples:**
- `d/dx[x²] = 2x`
- `d/dx[x³] = 3x²`
- `d/dx[x] = 1` (since `n=1`)
- `d/dx[x⁰] = 0` (since `n=0`, it's a constant)

> [!warning] IMPORTANT: Power Rule applies to the variable being differentiated, not to constants.
> - `d/dx[x²] = 2x` ✓
> - `d/dx[3²] = 0` (3² is a constant, `= 9`)

## 4. Sum Rule
$$
\frac{d}{dx}[f(x) + g(x)] = f'(x) + g'(x)
$$
Differentiate term by term
- Example: d/dx\[$x^2 + 3x$\] = 2x + 3


## 5. Chain Rule
$$
\frac{d}{dx}[f(g(x))] = f'(g(x)) \cdot g'(x)
$$
> [!important] In Words:
> Derivative of the **outer** function **times** the derivative of the **inner** function


# How to use Chain Rule

## Step-by-step method

- **Identify the composition.** What's the outer function? What's the inner function?
- **Differentiate the outer** with respect to its argument (treat the inner as a single variable).
- **Multiply by the derivative of the inner.**
- If there are more layers, keep multiplying.

### Example 1: $y = (3x + 1)^{2}$

Outer: $u^{2}$, Inner: $u = 3x + 1$
$$
\frac{dy}{du} = 2u, \frac{du}{dx} = 3
$$
Solving the whole thing:
$$
\frac{dy}{dx} = 2u \cdot 3 = 6u = 6(3x + 1) = 18x+6
$$

### Example 2: $y = (x^{2} + 1)^{3}$
Outer: $u^3$, Inner: $x^{2} + 1$

$$
\frac{dy}{dx} = 3u^{2} \cdot 2x = 3(x^{2} + 1)^{2} \cdot 2x = 6x(x^{2} + 1)^{2}
$$


# BackProp in Deep Learning

A neural network is a composition of functions:
$$
L = loss(f_3(f_2(f_1(x))))
$$
To get `∂L/∂w₁`, you multiply derivatives backward through each layer:
$$
​\frac{dL}{dw_1} = \frac{dL}{df_3} \cdot \frac{df_3}{df_2} \cdot \frac{df_2}{df_1} \cdot \frac{df_1}{dw_1}
$$
This is exactly the chain rule, just applied many times.

### Example: 2-layer network
```python
z1 = w1·x + b1
a1 = ReLU(z1)
z2 = w2·a1 + b2
L = (z2 − y)²
```
For `w1`:
$$
\frac{dL}{dw_1} = \frac{dL}{dz_2} \cdot \frac{dz_2}{da_1} \cdot \frac{da_1}{dz_1} \cdot \frac{dz_1}{dw_1}
$$
$$
= 2(z_2 - y) \cdot w_2 \cdot ReLU'(z_1) \cdot x
$$











































