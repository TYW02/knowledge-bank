
# What it does
- Tells us how well the model is doing


# Example
![[Pasted image 20230221155732.png]]

## Model: $f_w,_b(X) = wx + b$

### $w, b$: Parameters / Coefficients / Weights
Variables you can adjust during training in order to improve model


# What do $w, b$ do ?
![[Pasted image 20230221160107.png]]

## $w$ is the slope and $b$ is the y-intercept


![[Pasted image 20230221160326.png]]

# Find $w, b$: y-hat us close to $y^i$ for all ($x^i, y^i$)

## Cost function: (basic)
## (y-hat - y) = error


## Cost function: Squared error cost function
- Most commonly used for Linear Regression
![[Pasted image 20230221161207.png]]

### Can also be rewritten as:
![[Pasted image 20230221161243.png]]



# Cost Function Intuition
- Model: $f(x) = wx + b$
- Parameters: $w, b$
- Cost Function: Squared error function
- Goal: minimize $J(w,b)$

### Simplified
- Model: $f(x) = wx$
- Parameters: $w$
- Cost Function: ![[Pasted image 20230221161621.png]]
- Goal: minimize $J(w)$

![[Pasted image 20230221162016.png]]



![[Pasted image 20230221162436.png]]
For each value of $w$ you end up with a different points and its corresponding cost $J(w)$ and you can use these points to trace out this plot on the right.

![[Pasted image 20230221162714.png]]



![[Pasted image 20230221191755.png]]

















