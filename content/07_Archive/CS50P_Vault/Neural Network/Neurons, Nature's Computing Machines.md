
-------

# How does a neuron work ?
1. Takes electric input
2. Pops out another electrical signal
3. Output

- Neurons don't react readily, but instead suppress the input until it has grown so large that it triggers an output.
	- Think of this as an threshold that must be reached before any output is produced.
- Neurons don't want to be passing on tiny noise signals, only emphatically strong intentional signals.
![[Pasted image 20230323152714.png]]


# Activation Function

- A function that takes the input signal and generates an output signal, but takes into account some kind of threshold is called an #ActivationFunction.

- Mathematically, there are many such activation functions that could achieve this effect. A simple #StepFunction could do this:
![[Pasted image 20230323152915.png]]

---
- For low input values, the output is zero. However once the threshold input is reached, output jumps up.
- An artificial neuron behaving like this would be like a real biological neuron.
	- The term used by scientists actually describes this well, they say that neurons fire when the input reaches the threshold.

# Sigmoid Function

- The S-shaped funciton shown below is called the #SigmoidFunction
- Smoother than the cold hard step function, and this makes it more natural and realistic

![[Pasted image 20230323153436.png]]

---
- This smooth S-shaped sigmopid function is what we'll be contunue to use for making our own neural network.

>[!INFO] Attention !
>The Sigmoid function, sometimes also called the #LogisticFunction, is
>$$ y = \frac {1}{1+e^{-x}}$$

---
## Explanation of formula 

The letter $e$ is a mathematical constant 2.71828...

1. The input x is negated and e is raised to the power of that -x
2. The result is added to 1, so we have $$1 + e^{-x}$$
When x is 0, e^-x is 1 because anything raised to a power of zero is 1.
So y becomes 1 / (1 + 1) or simply 1/2. So the basic sigmoid cuts the y-axis at y =1/2

---

# Why we use sigmoid function
- The reason is that this function is much easier to do calculations with than other S-shaped functions



# Multiple inputs

> The first thing to realise is that real biological neurons take many inputs, not just one.
> We saw this when we had two inputs to the Boolean logic machine, so the idea of having more than one input is not new or unusual.

## What to do with all these inputs ?

- We simply combine them by adding them up, and the resultant sum is the input to the sigmoid funciton which controls the output.
- This reflects how real neurons work.
![[Pasted image 20230323154437.png]]

- If the combined signal is not large enough then the effect of the sigmoid threshold function is to suppress the output signal.
- If the sum x is large enough the effect of the sigmoid is to fire the neuron.
	- Interestingly, if only one of the several inputs is large and the rest small, this may be enough to fire the neuron.
	- What's more, the neuron can fire if some of the inputs are individually almost, but not quite, large enough because when combined the signal is large enough to overcome the threshold.
		- This gives you a sense of the more sophisticated, and in a sense fuzzy, calculations that such neurons can do.


> [!INFO] Attention !
> The thing to notice is that each neuron takes input from many before it, and also provides signals to many more, if it happens to be firing.
> 
> One way to replicate this from nature to an artificial model is to have layers of neurons, with each connected to every other one in the precdeing and subsequent layer. 


# Biological
![[Pasted image 20230323154938.png]]

# Artificial
![[Pasted image 20230323155004.png]]

# Explaining the architecture
---
You can see the three layers, each with three artificial neurons, or #Nodes. 
You can also see each node connected to every other node in the preceding and next layers.

## Which part does the learning ?
## What do we adjust in response to training examples ?
### Is there a parameter that we can refine like the slope of the linear classifier we looked at earlier ?

> [!INFO] Important !
> The most obvious thing is to adjust the strength of the connections between nodes.
> 
> Within a node, we could have adjusted the sum of the inputs, or we could have adjusted the shape of the sigmoid threshold function.
> 
> But that's more complicated than simply adjusting the strength of the connections between the nodes.

---

## Use a simple approach 

![[Pasted image 20230324165139.png]]

- The following diagram again shows the connected nodes, but this time a #Weight is shown associated with each connection.
	- A low weight will de-emphasise a signal, and a high weight will amplify it.

## Explaining the numbers next to the weight symbols

 # $$ w_2,_3$$
- This is simply the weight associated with the signal that passed between node 2 in a layer to node 3 in the next layer.

$$w_1,_2$$
- This is the weight that diminishes or amplifies the signal between node 1 and node 2 in the next layer

---


![[Pasted image 20230324165724.png]]

>[!INFO] Attention !
>- You might ask yourself why each node should connect to every other node in the previous and next layer.
>
>- They don't have to and you could connect them in all sorts of creative ways.
>
>- We don't because the uniformity of this full connectivity is actually easier to encode as computer instructions.


>[!INFO] Key Points:
>- Biological brains seem to perform sophisticated tasks like flight, finding food, learning language, and evading predators, despite appearing to have much less storage, and running much slower, than modern computers.
>
>- Biological brains are also incredibly resilient to damage and imperfect signals compared to traditional computer systems.
>
>- Biological brains, made of connected neurons, are the inspiration for artificial neural networks.

















