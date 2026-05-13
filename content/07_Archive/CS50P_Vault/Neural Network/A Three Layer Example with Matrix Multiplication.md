

# Example (3 Layers, 3 Nodes)
![[Pasted image 20230327143142.png]]

---
# Terminology

1. The first layer is the #InputLayer
2. The final layer is the #OutputLayer
3. The middle layer is the #HiddenLayer 
	- Because the outputs of the middle layer are not made apparent as outputs hence, the name

We can see the three inputs are 0.9, 0.1 and 0.8 
## Input Layer Matrix

$$ I = (0.9, 0.1, 0.8)$$
## Middle Hidden Layer
![[Pasted image 20230327143544.png]]
- We need to work out the combined (and moderated) signals to each node in this middle layer.
- This is the weights between the input and hidden layers
	- We need another matrix for the links between the hidden and output layers

## Hidden to Output weights
![[Pasted image 20230327143946.png]]


## Combined Moderated input to hidden layer
$$X_{hidden} = W_{input\_hidden} * I$$
![[Pasted image 20230327144138.png]]

---

# Visualisation of combined moderated inputs into second hidden layer
![[Pasted image 20230327144226.png]]
- These nodes apply a sigmoid activation function to make the response to the signal more like those found in nature.
$$O_{hidden} = sigmoid(X_{hidden})$$
- The sigmoid function is applied to each element in $X_{hidden}$ to produce the matrix which has the output of the middle hidden layer.
![[Pasted image 20230327144417.png]]

- You can also see that all the values are between 0 and 1, because this sigmoid doesn't produce values outside that range. Look back at the graph of the logistics function to see this [[Neurons, Nature's Computing Machines#Sigmoid Function|Visually]]

We've worked out the signal as it passes through the middle layer. That is, the outputs from the middle layer. Which, just to be super clear, are the combined inputs into the middle layer which then have the activation fucntion applied.

![[Pasted image 20230327144907.png]]
- The inputs into this layer are the outputs from the second layer we just worked out $O_{hidden}$ And the weights are those for the links between the second and third layers $W_{hidden\_output}$ not those we just used between the first and second.
$$X_{output} = W_{hidden\_output} * O_{hidden}$$
![[Pasted image 20230327145126.png]]

- The updated diagram now shows our progress feeding forward the signal from the initial input right through to the combined inputs to the final layer.

![[Pasted image 20230327145217.png]]

- All that remains is to apply the sigmoid activation function, which is easy.
![[Pasted image 20230327145245.png]]


# Final Diagram
![[Pasted image 20230327145301.png]]

> [!INFO] Next Step:
> - Use the output from the neural network and compare it with the trainging example to work out an error.
> 
> - We need t use that error to refine the neural network itself so that it improves its outputs.


































