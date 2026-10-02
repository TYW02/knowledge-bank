# Softmax
- Returns **logits**, a set of probabilities that add up to **1**
- **Multi-Class** Classification: Since each, class's probability has to add up to 1 
## Formula

> [!important] Formula for Single Softmax
> $$
> \frac{e^{i}}{\sum{e^{j}}}
> $$
- When we take the **Sum of Softmax** we take the Sum of **ALL the softmax calculation** we have done.

> [!important] This is what is looks like
> $$
> \sum\frac{e^{i}}{\sum{e^{j}}}
> $$
> We can move the **Sum** up to the **numerator** and **evaluates to the same** as the **denominator**.
> - This means that we are essentially taking the **same number divided by itself**.
> - Hence we get **1.**


























































