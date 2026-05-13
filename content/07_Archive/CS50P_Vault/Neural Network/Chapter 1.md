
# What a neuron output does
- What it does it it takes a fraction of the input value, then adds the bias.
	- All the neuron does is take the fractions of inputs, where these fractions (weights) are the adjustable parameters, and adds another adjustable parameter - the bias - then outputs the result.

```python
output = (inputs[0] * weights[0] +
		  inputs[1] * weights[1] +
		   inputs[2] * weights[2] + bias)
print(output)

>>> 2.3
```




# A Layer of Neuron

- What are layers ?
	- Layers are nothing more than a group of neurons.
		- Each neuron in a layer takes exactly the same input (the input given to the layer [either training data or output from previous layer]), but contains its own set of weights and its own bias, thus producing its own unique output.


# What is the computer doing ?

- Computers don't really think, they're just glorified calculators 

## Imagine a machine that converts kilometers to miles

kilometres --> calculate ??? --> miles

We don't know the formula for converting them, all we know is that the relationship is **linear**.
	- this gives us a clue that the formula needs to be "miles = kilometres x C" where c is a constant

| Truth Example | Kilometres | Miles |
| ------------- | ---------- | ----- |
| 1             | 0          | 0     |
| 2             | 100        | 62.137      |

### What should we do to work out that missing constant c ?
- Let's just pluck a value at random and give it a go

Kilometres (100) --> miles = kilometres x (0.5) --> miles (50)
- This is not exactly right because our truth example 2 tells us the answer should be 62.137

# How wrong are we ?

We're wrong by 12.137. That's the **error**, the difference between our calculated answer and the actual truth from our list of examples.

## $$ error = truth - calculated$$
## $$ = 62.137 - 50 $$ $$ = 12.137 $$
## What to do with error
- We use this error to guide a second, better, guess at c

>[!INFO] LOOK AT THAT ERROR AGAIN.
>We were short by 12.137, we know that increasing c will increase the output.
>Let's nudge c up from 0.5 to 0.6 and see what happens.


Kilometres (100) --> miles = kilometres x (0.6) --> calculated miles (60)
correct miles (62.137)
error (2.137)

> [!INFO] Important note.
> We used the error to guide how we nudged the value of c.


Kilometres (100) --> miles = kilometres x (0.7) --> calculated miles (70)
correct miles (62.137)
error (-7.863)

> Oh no ! We've **overshot** the known correct answer.
> Our previous error was 2.137 but now it's -7.863
> The minus sign simply says we overshot rather than undershot. 


> [!INFO] Important note.
> We should moderate how much we nudge the value of c. If the outputs are getting close to the correct answer (error getting smaller).
> 
> Then don't nudge the changeable bit so much.


### This repeated process is the core process of learning in a neural network.


> [!INFO] Key Points:
> - All useful computer systems have an input, and an output, with some kind of calculation in between. Neural networks are no different.
> - When we don't know exactly how something works we can try to estimate it with a model which includes parameters which we can adjust. If we didn't know how to convert kilometres to miles, we might use a linear function as a model, with an adjustable gradient.
> - A good way of refining these models is to adjust the parameters based on how wrong the model is compared to known true examples.
