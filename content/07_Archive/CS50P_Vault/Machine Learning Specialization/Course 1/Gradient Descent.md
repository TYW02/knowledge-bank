
- Used to find value of w b 
- Algorithm used to minimize and function not just a **cost function** for linear regression (NOT A COST FUNCTION)

## Have some function $J(w, b)$
### Want min $J(w, b)$

## Outline:
- Start with some $w, b$ mainly set to 0 
- Keep changing $w, b$ to reduce $J(w, b)$
- Until we settle at or near a minimum (May have > 1 minimum)


# Implementing Gradient Descent

## Gradient Descent Algorithm

# $w = w - α$ $* \frac {d}{dw} J(w,b)$
# $b = b - α$ $* \frac {d}{db} J(w,b)$
- These 2 algorithms are repeated until they converge (reach the point at the local minima where the parameter w and b no longer change much with each step you take)
- Simultaneously update w and b
----
## For finding minimum w value

## What = means
- This is an Assignment operator not a truth assertion


## What does α mean
- Learning Rate 
- Controls how big of a step you take downhill
- Bigger alpha value means more aggressive descent


## What does $\frac {d}{dw} J(w,b)$ mean
- This is the derivative term of the cost function $J$ 
- Telling you which direction you should descent 
- In combination with α tells you size of the step you should take downhill


## What this means $- α$ $* \frac {d}{dw} J(w,b)$
- Update Parameter W by taking current value of W and adjusting it a small amount 
----


# Correct: Simultaneous Update

## tmp_w = $w - α$ $* \frac {d}{dw} J(w,b)$
## tmp_w $= b - α$ $* \frac {d}{db} J(w,b)$
## w = tmp_w
## b = tmp_b




# Gradient Descent Intuition
![[Pasted image 20230226181336.png]]

## $\frac {d}{dw} J(w)$ is basically finding the slope
- When the Slop is positive $w$ will decrease
- When the Slope is negative $w$ will increase








































