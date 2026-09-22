> [!Definition]
> Regularization technique that randomly turns off nodes and their connections during training to prevent a neural network from overfitting.

> [!Warning]
> Better not to use if your batch size is small



## How does Dropout work

- Training Phase: For every **training step**, the model randomly selects a **percentage** of nodes and sets their **output to zero**. This creates a temporary, smaller sub-network
- Backward Pass: Weight updates during **backpropagation** **ONLY** apply to the **active nodes** that were kept in that **specific step**
- Testing / Inference Phase: Dropout is **turned off**. The full network is used, but all **activation** are **scaled down** by the **dropout probability** factor to **balance the output values**.


## Why we use it
- Prevents overfitting: Stops model from **memorizing** the training data noise and **forces** it **learn real**, generalized patterns
- Stops Co-adaptation: Stops neighbouring nodes from **relying too much** on each other or **fixing one another's mistakes**, making every single node more **robust** on its own
- Ensemble Effect: Training with dropout is **similar** to training a massive collection of **different thin** networks and **averaging their final predictions**.






























































