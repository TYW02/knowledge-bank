

![[Pasted image 20230324170300.png]]

- Just as before, each node turns the sum of the inputs into an output using an activation function.
- We'll also use the sigmoid function that we saw before, where x is the sum of incoming signals to a neuron, and y is the output of that neuron.
$$y = \frac {1}{(1 + e^{-x})}$$

### What about the weights ?
Let's start with some random weights
- w1,1 = 0.9
- w1,2 = 0.2
- w2,1 = 0.3
- w2,2 = 0.8

- Random starting values aren't such a bad idea, and it is what we did when we chose an intial slope value for the simple linear classifiers earlier on.
- The random value got improves with each example that the classifier learned from.

There are only 4 weights in this small neuron network, as that's all the combinations for connecting the 2 nodes in each layer.
![[Pasted image 20230324170817.png]]

1. The first layer of nodes is the input layer, and it doesn't do anything other than represent the input signal. (No calculations to be done here.)
2. For each node in this layer we need to work out the combined input. As x in the sigmoid function is the combined input into a node.
	- Let's focus on node 1 in the layer 2, Both nodes in the first input layer are connected to it.
	- Those input nodes have raw values of 1.0 and 0.5
		- The link from the first node has a weight of 0.9 associated with it.
		- The link from the 2nd node has a weight of 0.3
### x = (output from first node * link weight) + (output from second node * link weight)
$$ x = (1.0 * 0.9) + (0.5 * 0.3)$$
$$x = 0.9 + 0.15$$
$$x = 1.05$$
- Now we've got x = 1.05 for the combined moderated input into the first node of the second layer.
- Calculate that node's output using the activation function
	- y = 1 / (1 + 0.3499)
	- y = 0.7408

![[Pasted image 20230324171744.png]]





























































