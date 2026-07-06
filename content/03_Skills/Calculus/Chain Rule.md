---
title: Chain Rule
---
If $f(u)$ if a function of variable u, and if $u(x)$ is also a function, then chain rule can be applied.
In order to find $f(u(x))$

$\frac{\partial f}{\partial x} = \frac{\partial f}{\partial u} \frac{\partial u}{\partial x}$

> [!NOTE]
> $f(u)$ is called the outside function
> $u(x)$ is called the inside function

Chain rule states that df/dx = (df/du) * (du/dx)

### Worked Example
$\frac{\partial}{\partial x}(2x^2 - 5)^5$
> [!Solution]
> We let $u = 2x^2 - 5$
> Now the problem looks like: $f(u) = u^5, u(x) = 2x^2-5$
> $[\frac{\partial}{\partial u}(u^5)]* [\frac{\partial}{\partial x}(2x^2-5)]$
> = $(5u^4)(4x) = 20xu^4$
> Then we sub in $u$
> = $20x(2x^2-5)^4$

