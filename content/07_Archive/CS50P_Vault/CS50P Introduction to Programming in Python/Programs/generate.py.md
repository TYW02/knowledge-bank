Tags: [[Lecture 4 - Libraries]]



## Using random.choice
```python
import random

coin = random.choice(["heads", "tails"])
print(coin)

> Output: heads
> Output: heads
> Output: tails
```


## Using from
```python
from random import choice

coin = choice(["heads", "tails"])
print(coin)

> Output: heads
> Output: heads
> Output: tails
```


## randint()
```python
import random

number = random.randint(1, 10)
print(number)

> Output: 4
> Output: 8
> Output: 10
```


## shuffle()
```python
import random

cards = ["jack", "queen", "king"]

random.shuffle(cards)
for card in cards:
	print(card)

> Output: queen
> king 
> jack

```










