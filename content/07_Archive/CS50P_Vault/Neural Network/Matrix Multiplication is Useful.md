> Previously we manually did the calculations for a 2-layer network with just 2 nodes in each layer.
> That was enough work, but imagine doing the same for a network with 5 layers and 100 nodes in each ?

## So how can matrices help ?
1. They allow us to compress writing all those calculations into a very simple short form.
2. Many computing programming languages understand working with matrices, and because the real work is repetitive, they can recognise that and do it very quickly and efficiently.

- In short, matrices allow us to express the work we need to do concisely and easily, and computers can get the calculations done quickly and efficiently.

# What is a matrix ?
- A #Matrix is just a table, a rectangular grid, of numbers. That's it. There's nothing much more comples about a matrix than that.

## Example
![[Pasted image 20230324175203.png]]

- That's a matrix - a table or a grid of numbers - just like the following example of a matrix of size "2 by 3".

![[Pasted image 20230324175244.png]]

- It is convention to use rows first then columns, so this isn't a "3 by 2" matrix, it is a "2 by 3" matrix.


# Simple matrix multiplication
![[Pasted image 20230324175411.png]]

- You can see that we don't simply multiply the corresponding elements.

![[Pasted image 20230324175515.png]]



> [!INFO] Important Limit !!
> You can't just multiply any 2 matrices, they need to by compatible.
> 
> If the number of elements in the rows don't match the number of elements in the columns then the method doesn't work.
> 
> So you can't multiply a "2 by 2" matrix by a "5 by 5" matrix.
> 
> To multiply matrices the number of columns in the first must be equal to the number of rows in the second.


# Dot product
- In some guides, you'll see this kind of matrix multiplication called a #DotProduct or an #InnerProduct. There are actually different kinds of multiplication possible for matrices, such as a cross product, but the dot product is the one we want here.


![[Pasted image 20230324180027.png]]

- The first matrix contains the weights between nodes of two layers.
- The second matrix contains the signals of the first input layer.
- The answer we get by multiplying these 2 matrices is the combined morderated signal into the nodes of the second layer.
	- Look carefully, and you'll see this, the first node moderated by the weight w1,1 added to the second input_2 moderated by the weight w2,1
	- These are the values of x before the sigmoid activation function applied.

![[Pasted image 20230324180311.png]]

# Why it is useful
- We can express all the calculations that go into working out the combined moderated signal, x, into each node of the second layer using matrix multiplication.
$$X = W . I$$
- W is the matrix of weights
- I is the matrix of inputs
- X is the resultant matrix of combined moderated signals into layer 2 


# What about the activation function ?
- All we need to do is apply the sigmoid function to each individual element of the matrix X
	- That sounds too simple, but it is correct because we're not combining signals from different nodes here, we've already done that and the answers are in X.
	- As we saw earlier, the activation function simply applies a threshold and squishes the response to be more like that seen in biological neurons.
$$O = sigmoid(X)$$
- O is a matrix, which contains all the outputs from the final layer of the neural network.

The expressions X = W . I applies to the calculations between one layer and the next.
If we have 3 layers, for example, we simply do the matrix multiplication again, using the outputs of the second layers as inputs to the third layer but of course combined and moderated using more weights.

>[!INFO] Key Points:
>- The many calculations needed to feed a signal forward through a neural network can be expressed as #MatrixMultiplication 
>
>- Expressing it as matrix multiplication makes it much more consice for us to write, no matter the size of neural network.
>
>- More importantly, some computer programming languages understand matrix calculations, and recognise that the underlying calculations are very similar. This allows them to do these calculations more efficiently and quickly.
















































