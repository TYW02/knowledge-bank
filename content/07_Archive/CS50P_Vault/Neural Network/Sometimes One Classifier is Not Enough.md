

## Example
| Input A | Input B | Logical AND | Logical OR |
| ------- | ------- | ----------- | ---------- |
| 0       | 0       | 0           | 0          |
| 0       | 1       | 0           | 1          |
| 1       | 0       | 0           | 1          |
| 1       | 1       | 1           | 1           |



![[Pasted image 20230323151000.png]]

---
- Look at the following plot, showing the two inputs A and B to the logical function as coordinates on a graph.
- The plot shows that only when both are true, with value 1, is the output also true, shown as green.
	- False outputs are shown red.
---

You can also see a straight line that divides the red from the green regions.
That line is a linear function that a linear classifier could learn, just as we have done earlier.


## Boolean OR function 
![[Pasted image 20230323151258.png]]
Only (0,0) point is red because it corresponds to both inputs A and B being false.

The beauty of the diagram is that it makes clear that it is possible for a linear classifier to learn the Boolean OR function too.

# Boolean XOR
- Stands for eXclusive OR 
	- Only has a true output if either one of the inputs A or B is true, but not both.
		- When the inputs are both false, or both true, the output is false.

| Input A | Input B | Logical XOR |
| ------- | ------- | ----------- |
| 0       | 0       | 0           |
| 0       | 1       | 1           |
| 1       | 0       | 1           |
| 1       | 1       | 0            |

## Function plot on grid
![[Pasted image 20230323151655.png]]

> [!INFO] Important !!
> This is a challenge !
> We can't seem to separate the red from the bule regions with only a single straight dividing line.

- Impossible to have a straight line that successfully divides the red from the green regions for the Boolean XOR.
- A Simple linear classifier can't learn the Boolean XOR if presented with training data that was governed by the XOR function.


# What is the fix ? 
![[Pasted image 20230323151921.png]]

---
## We use Multiple Classifiers working together
- Diagram has 2 straight lines to separate out the different regions suggests the fix
- Many linear lines can start to separate off even unsuaully shaped regions for classification.
---


> [!INFO] Key Points:
> - A simple linear classifier can't separate data where that data itself isn't governed by a single linear process. For Example, data governed by the logical XOR operator illustrates this.
> - However the solution is easy, you jsut use mutiple linear classifiers to divide up data that can't be separated by a single straight dividing line.





























































