
# Definition
$\frac{1}{1 + e^{-f(x)}}$
- Maps any input value into a smooth S-shaped range between \[0, 1]
- Binary Classification: Used in final output layer or in Logistic Regression when outcome must be classified into 1 of 2 groups \[yes / no]
- DOES NOT SUM TO 1
- Can be interpreted as Probabilities


## How to Derive
![[Sigmoid Derivation.svg]]


### Example
- g(0) = 0.5

> Derivative of sigmoid is g(x)(1 - g(x))
> 
> 0.5 * (1 - 0.5) = 0.25


































































