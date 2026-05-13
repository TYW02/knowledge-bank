

# What happens when α is too small

## $w = w - α \frac {d}{dw}J(w)$
- The derivative term is multiplied by a really small number 
![[Pasted image 20230226183945.png]]
- Each step will be really small resulting in a longer training time


# What happens when α is too large
![[Pasted image 20230226184208.png]]
- Each step will be too big resulting in overshooting the minimum 
- Fail to converge might diverge instead


# What will happen when you reach a mimimum
![[Pasted image 20230226184602.png]]
- When you have already reached a minimum (slope = 0), Gradient Descent will update the new $w$ value as itself.


# What happens during Gradient Descent
![[Pasted image 20230226184926.png]]
- When starting at large value the derivative will be a large value as the slope is steeper
- As $w$ gets closer to the minimum the derivative becomes smaller and the steps become smaller.









































