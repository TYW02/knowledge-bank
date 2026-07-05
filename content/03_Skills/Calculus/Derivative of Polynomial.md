---
title: Derivative of Polynomial
---
Given a polynomial term in the form of $ax^b$ where `a` is a constant and `b` is a constant exponent.

### Derivative with respect to variable x
1. Multiply coefficient `a` by exponent `b`
2. Reduce exponent by `1` 

### Example
$\frac{\partial}{\partial x}(ax^b) = bax^{b-1}$ 

### Variable in denominator
$\frac{1}{x^n} = x^{-n}$ 

### Worked Example 1
Perform following derivative with respect to X
$\frac {\partial}{\partial x}(5x^3)$
> [!Solution]-
> $(3)(5)x^{3-1}$
> $15x^2$

### Worked Example 2
Perform the following derivative with respect to t
$\frac {\partial}{\partial t}(t^4)$
> [!Solution]-
> $4t^{4-1}$
> $4t^{3}$

### Worked Example 3
Perform the following derivative with respect to x
$\frac {\partial} {\partial x}(6x^{\frac{2}{3}})$
> [!Solution]-
> $(\frac{2}{3})(6)x^{\frac{2}{3} - 1}$
> $4x^{\frac{2}{3} - 1}$
> $4x^{\frac{-1}{3}}$
> Remember that $x^{\frac{-1}{3}}$ = $\frac{1}{x^{\frac{1}{3}}}$
> $\frac{4}{x^{\frac{1}{3}}}$

### Worked Example 4
Perform the following derivative with respect to u
$\frac{\partial}{\partial u}(\frac{7}{u})$
> [!Solution]-
> $7u^{-1}$
> $(-1)(-7)u^{-1-1}$
> $-7u^{-2}$
> $-\frac{7}{u^{2}}$

### Worked Example 5
Perform the following derivative with respect to x
$\frac{\partial}{\partial x}(\sqrt{3x})$
> [!Solution]-
> $(3x)^{\frac{1}{2}}$
>$3^{\frac{1}{2}}x^{\frac{1}{2}}$
>Take note this ^ is basically $ax^b$
>$(\frac{1}{2})(3^{\frac{1}{2}})x^{\frac{1}{2} - 1}$
>Note: $(\frac{1}{2})(3^{\frac{1}{2}}) = \frac{3^{\frac{1}{2}}}{2}$
>
>$\frac{3^{\frac{1}{2}}}{2}x^{-\frac{1}{2}}$

### Worked Example 6
Perform the following derivative with respect to x
$\frac{\partial}{\partial x}(6x^3 - 12x)$
> [!Solution]-
> Here we have 2 terms, to solve this we find the derivatives of **EACH** term and **ADD** them together.
> $\frac{\partial}{\partial x}(y_1 + y_2) = \frac{\partial y_1}{\partial d} + \frac{\partial y_2}{\partial x}$
> **Solving Individual Derivatives:**
> Solving $y_1$
> $6x^3$
> $(3)(6)x^{3-1}$
> $18x^{2}$
> Solving $y_2$
> $-12x$
> $(1)(-12)x^{0}$
> $-12x^{0}$
> $-12$
>** Putting it together:** $\frac{\partial y_1}{\partial d} + \frac{\partial y_2}{\partial x}$
> $18x^{2} + (-12)$
> = $18x^{2} -12$





