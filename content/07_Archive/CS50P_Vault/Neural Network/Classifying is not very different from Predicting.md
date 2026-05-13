![[Pasted image 20230322160823.png]]

- In the plot above, if the line was dividing the caterpillars from the ladybirds, then it could be used to classify an unknown bug based on its measurements. 

- The line above doesn't do this yet because half the caterpillars are on the same side of the dividing line as the ladybirds.



![[Pasted image 20230322161023.png]]

- That's much better ! This line neatly separates caterpillars from ladybirds. We can now use this line as a #Classfier of bugs

> [!INFO] Assumption.
> We are assuming that there are no other kinds of bugs that we haven't seen - but that's ok for now, we're simply trying to illustrate the idea of a simple classifier.


# Training A Simple Classifier

We want to **train** our linear classifier to correctly classify bugs as ladybirds or caterpillars. We saw above this is simply about refining the slope of the dividing line that separates the two groups of points on a plot of bug width and height.

## How do we do this ?

| Example | Width | Length | Bug      |
| ------- | ----- | ------ | -------- |
| 1       | 3.0   | 1.0    | Ladybird |
| 2       | 1.0   | 3.0    | Caterpillar         |

This is a set of examples which we know to be the truth.
It is these examples which will help refine the slope of the classifier function.
Examples of truth used to teach a predictor or a classifier are called the #TrainingData.


![[Pasted image 20230322162059.png]]

### $$ y = Ax $$
> [!INFO] Information on formula 
> - This is simpler than the fuller form for a straight line.
> - y = Ax + B
> - Having a non-zero B simply means the line doesn't go through the origin of the graph, which doesn't add anything useful to our scenario.

- We saw before that the parameter A controls the slope of the origin.
- The larger A is, the larger the slope.

- Let's go for A = 0.25 to get started. The dividing line is y = 0.25x. 
- Let's plot this line on the same plot of training data to see what it looks like:


![[Pasted image 20230322162527.png]]


- We can see that the line y =  0.25x isn't a good classifier already without the need to do any calculations.
- The line doesn't divide the two types of bug. 
- We can't say "if the bug is above the line then it is a caterpillar" because the ladybird is above the line too.

# Let's look at the first training example

### $$ y = (0.25) * (3.0) = 0.75 $$
- The function, with the parameter A set to the initial randomly chosen value of 0.25, is suggesting that for a bug of width 3.0, the length should be 0.75. 
- We know that's too small because the training data example tells us it must be a length of 1.0
	- So we have a difference, an error. Just as before, we can use this error to inform how we adjust the parameter A.


- So the desired target is 1.1 and the error E is 

error = (desired target - actual output)
$$ E  = 1.1 - 0.75 = 0.35 $$ 

# How is A related to E ?

$$ y = Ax $$
- We know that for initial guesses of A this gives the wrong answer for y, which should be the value given by the training data. 
- Let's call the correct desired value, t for target value.
	- To get that value t, we need to adjust A by a small amount.
		- Mathematicians use the delta symbol $\delta$ to mean "a small change in"

$$ t = (A + \delta A)x $$

![[Pasted image 20230322163909.png]]


- Remember the error E was the difference between the desired correct value and the one we calculate based on our current guess for A. That is, E was t - y

$$ t - y = (A + \delta A)x - Ax$$
- Expanding out the terms and simplifying
$$ E = t - y = Ax + (\delta A)x - Ax$$
$$ E = (\delta A)x $$

# What we want 
- We wanted to know how much to adjust A by to improve the slope of the line so it is a better classifier, being informed by the error E. 
- To do this we simply re-arrange that last equation to put $\delta$ A on it's own.
$$ \delta A = E / x$$
 0.35 / 3.0 = 0.1167 that means we need to change the current A = 0.25 by 0.1167.
 This means the new improved value for A is 0.25 + 0.1167 = 0.3667.


![[Pasted image 20230322164707.png]]


- It hasn't divided the region between ladybirds and caterpillars.

#### How do we fix this ?
- We moderate the updates. That is, we calm them down a bit. Instead of jumping enthusiastically to each new A, we take a fraction fo the change $\delta A$, not all of it. 
- This way we move in the direction that the training example suggests, but do so slightly cautiously.

- This moderation, has another very powerfu and useful side effect. When the training data itself can't be trusted to be perfectly true, and contains errors or noise, both of which are normal in real world measurements, the moderation can dampen the impact of those errors or noise. It smooths them out.


### Adding a moderation into the update formula
$$ \delta A = L (E / x)$$
> [!INFO] Moderation
> The moderating factor is often called a #LearningRate, and we've called it L. Let's pick L = 0.5 as a reasonable fraction just to get started. 
> It simply means we only update half as much as would have done without moderation.

Running through that all again, we have an initial A = 0.25. y = 0.25 * 3.0 = 0.75 A desired value for 1.1 gives us an error of 0.35. The $\delta A = L (E / x)$ = 0.5 * 0.35 / 3.0 = 0.0583,
The updated A is 0.25 + 0.0583 = 0.3083

![[Pasted image 20230322165628.png]]

> [!INFO] Key Points:
> - We can use simple maths to understand the relationship between the output error of a linear classifier and the adjustable slope parameter. That is the same as knowning how much to adjust the slope to remove that output error.
> - A problem with doing these adjustments naively, is that the model is updated to the best match the last training example only, effectively ignoring all previous training examples. A good way to fix this is to moderate the updates with a learning rate so no single training example totally dominates the learning.
> - Training examples from the real world can be noisy or contain erorrs. Moderating updates in this way helpfully limits the impact of these false examples.







