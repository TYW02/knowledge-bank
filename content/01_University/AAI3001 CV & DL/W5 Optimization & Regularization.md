---
title: W5 Optimization & Regularization
---

---
- [[#Optimization Challenges in Deep Learning|Optimization Challenges in Deep Learning]]
	- [[#Optimization Challenges in Deep Learning#Saddle Point|Saddle Point]]
	- [[#Optimization Challenges in Deep Learning#Critical Point|Critical Point]]
	- [[#Optimization Challenges in Deep Learning#Stochastic Gradient Descent (SGD)|Stochastic Gradient Descent (SGD)]]
	- [[#Optimization Challenges in Deep Learning#SGD + Momentum|SGD + Momentum]]
	- [[#Optimization Challenges in Deep Learning#Adaptive Learning Rate - RMSProp|Adaptive Learning Rate - RMSProp]]
	- [[#Optimization Challenges in Deep Learning#Adam|Adam]]
	- [[#Optimization Challenges in Deep Learning#Learning Rate Schedule|Learning Rate Schedule]]
- [[#RMSProp|RMSProp]]
- [[#Adam: RMSProp + Momentum|Adam: RMSProp + Momentum]]
- [[#Learning Rate Decay|Learning Rate Decay]]
- [[#Warm Up|Warm Up]]
	- [[#Warm Up#Specify the optimization algorithm|Specify the optimization algorithm]]
	- [[#Warm Up#L1 Regularization|L1 Regularization]]
	- [[#Warm Up#L2 Regularization|L2 Regularization]]
- [[#Training Instability|Training Instability]]
- [[#Data preprocessing for images|Data preprocessing for images]]
- [[#Weight Initialization|Weight Initialization]]

---

# How to select a good training model ?

> [!important] Plot Training and Validation or Test Loss
> - **Training** and **Validation** loss should be decreased gradually
> - Stop training if **validation** loss does not decrease for several iterations (Tolerance)

> The goal of deep learning is to reduce the **generalization** error (Error on **Validation or Test** datasets)

![[Pasted image 20261006174023.png]]


# N-fold Cross Validation for Model Selection

![[Pasted image 20261006174055.png]]




# Optimization

## Optimization Challenges in Deep Learning

- Almost all optimization issues arising in deep learning are **non-convex**

### Saddle Point

> [!term] Saddle Point
> - **Any location** where **all gradients** of a function **vanish** but which is **neither** a **global nor a local minimum**

![[Pasted image 20261006174953.png]]
### Critical Point
> [!term] Critical Point
> - Gradient is **close to zero**
> - **BOTH** local minimum and saddle point are the **critical points**

![[Pasted image 20261006175019.png]]


# How to improve optimization ?

### Stochastic Gradient Descent (SGD)
> [!important] Stochastic Gradient Descent
> ```python
> torch.optim.SGD(params, lr=0.001)
> ```

### SGD + Momentum
> [!important] SGD + Momemtum
> ```python
> torch.optim.SGD(params, lr=0.001, momentum=0.9)
> ```

### Adaptive Learning Rate - RMSProp

### Adam
> [!important] Adam: Momentum + RMSProp
> ```python
> torch.optim.Adam(params, lr=0.001, betas=(0.9, 0.999))
> ```

### Learning Rate Schedule


![[General Guide]]

# Gradient Descent with Batch

![[Pasted image 20261006175710.png]]

> [!question] How does Stochastic Gradient Descent compute ?
> - Use 1 sample
> - Or a **batch** like B = 32
> - 1 epoch = **see all** the batches **once**
> - **Shuffle after** each epoch

![[Pasted image 20261006175731.png]]

> [!warning] GD
> - Uses **set of ALL** training data samples to compute the **gradient in each step**.


# Stochastic Gradient Descent (SGD)

> [!note] Characteristics
> - Full-batch is often **too costly** to compute a gradient and **easy to get stuck**
> - SGD is a **noisy approximated version** of the full batch gradient, "**noisy**" update is **better for training**

![[Pasted image 20261006180324.png]]

![[Pasted image 20261006180339.png]]

> [!note]
> Here we first **calculate the gradient**, and when we take the **next step** we use the **negative of that gradient** or basically go **opposite of the gradient**.


# Momentum

> [!note] High level description
> Control the **amount of parameter changes** to achieve **effective optimization**

```python
torch.optim.SGD(params, lr=0.001, momentum=0.9)
```

![[Pasted image 20261006180641.png]]

> The new update, is based on **LAST STEP - PRESENT GRADIENT**

![[Pasted image 20261006180823.png]]

> [!note]
> By taking the **previous step into account**, even if our **current gradient is SMALL**, we can still move out even if there is a **saddle point**

![[Pasted image 20261006181018.png]]


# What does Momentum do ?

> [!important] Characteristics
> - Acts as a **memory** for gradients in the **past**, applied gradient is **stabilized** by an **average from the past**
> - It can help in **flat valleys** because it remembers the **bigger movement** from the **past steps.**

![[Pasted image 20261006181305.png]]

> [!note]
> This is like, if the **current gradient is small,** you **add the previous movement** to it, which can help you move out of certain "**Spots**"


# Adaptive Learning Rate

> [!important] Key Idea
> You use the same learning rate for all parameters.
> - BUT at different points in training, different steps sizes will also affect your training

![[Pasted image 20261006182046.png]]


## RMSProp

> [!warning] Criteria
> - If gradient is **small** (flat region), then **increase the learning rate**
> - If gradient is **large** (steep region), then **decrease the learning rate**

![[Pasted image 20261006182324.png]]

![[Pasted image 20261006182445.png]]


## Adam: RMSProp + Momentum

```python
torch.optim.Adam(model.parameters(), lr=0.001, betas=(0.9, 0.999))
# NOTE: betas=(momentum, RMSProp)
```

# Optimization Summary

![[Pasted image 20261006182639.png]]

# Learning Rate Schedule

## Learning Rate Decay

> [!important] Main Idea: Learning Rate Decay
> - As **training goes on**, we are **closer to the destination,** so we **reduce the learning rate**

## Warm Up

> [!important] Main Idea: Warm Up
> - **Increase** and **then decrease**, at the **beginning**, do exploration
> 

![[Pasted image 20261006183035.png]]

![[Pasted image 20261006183049.png]]


# Optimizer in PyTorch

### Specify the optimization algorithm
```python
optimizer = optim.SGD(model.parameters(), lr=lr, momentum=0.9)
```

```python
outputs = model(inputs)
loss = criterion(outputs, labels)

# Reset accumulated gradients
optimizer.zero_grad()

# Compute new gradients
loss.backward()

# Apply new gradients to change model parameters
optimizer.step()
```


```python
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)
scheduler = StepLR(optimizer, step_size=2) # Example learning rate scheduler

# Train epochs
for epoch in range(num_epochs):
	model.train()
	running_loss = 0.0
	for inputs, labels in train_loaderL
		inputs, labels = inputs.to(device), labels.to(device)
		optimizer.zero_grad()
		outputs = model(inputs)
		loss = criterion(outputs, labels)
		loss.backward()
		optimizer.step()
		running_loss += loss.item()
		
	# Record train loss
	train_losses.append(running_loss / len(train_loader))
	print(f"Epoch [{epoch+1}/{num_epochs}], Loss:{running_loss/len(train_loader):.4f}")
	
	# Step the scheduler
	scheduler.step() 
	# Usually called once per epoch, after step_size calls, reduce learning rate by a factor
```


---

# Regularization & Weight Initialization


# Overfitting

> [!important] Main Idea: Overfitting
> - A model with high capacity **fits the noise** in the data **instead** of the **underlying relationship**

![[Pasted image 20261006184804.png]]

> Model may fit the training data very well, but fails to **generalize** to test data

![[Pasted image 20261006184830.png]]


# Data Augmentation

> [!important] Main Idea: Data Augmentation
> - Create **new data derived** from the **training data set**
> - Can **not be done casually**, should **make sense** for your **testing scenario**

![[Pasted image 20261006185006.png]]


# Early Stopping

> [!important] Main Idea: Early Stopping
> - During model training, use a validation set, along with the training set
> - **Stop** when the **validation accuracy** (or loss) has **not improved** after `n` subsequent epochs
> - The parameter `n` is called **patience** (**tolorance**)

![[Pasted image 20261006185232.png]]

> Cut the training before the model overfits


# Regularization: Weight Decay

> [!important] Weight Decay
> Overfitting usually **requires larger weights** to account for "large curvature"
> - Weights should be **small** but **not too small**

![[Pasted image 20261006190011.png]]


![[Pasted image 20261006190104.png]]

### L1 Regularization
> [!important] Characteristics
> Encourages **sparsity** by adding a penalty proportional to the absolute value of the model's weights, which **drives many weights** down to an **exact value of zero.**
> - L1 Encourages $\theta = [1, 0, 0, 0]$

### L2 Regularization
> [!important] Characteristics
> Encourages **distributed small weights** because it **penalizes the square of the weights**. Which causes the penalty to **shrink larger weights aggressively**, while **leaving small weights virtually untouched** rather than driving them to 0.
> - L2 Encourages $\theta = [0.25, 0.25, 0.25, 0.25]$

![[Pasted image 20261006190713.png]]

> [!note]
> Here we see that if the weight decay is TOO LOW, the model looks like its overfitting
> - Whereas if the coefficient it TOO HIGH, the model could ignore certain relationships


# Dropout

> [!important] Main Idea: Dropout
> - **Randomly drop nodes** (along with their connections) during **training**. Typically, **disable dropout at test** time
> - Each node is retained with a **fixed dropout rate**, **independent** of other nodes
> - Typical choices: 20% of the input nodes and 50% of the hidden nodes

![[Pasted image 20261006191014.png]]


# Mismatch

> [!important] Main Idea: Mismatch
> - Your **training** and **testing** data have **different distributions**
> - Be aware of **how data is generated**

![[Pasted image 20261006191158.png]]


# Numerical Stability & Initialization

## Training Instability
- **Training** and **validation** loss should be **decreased gradually**, but not always

![[Pasted image 20261006191303.png]]

## Data preprocessing for images

```python
test_transforms = torchvision.transforms.Compose([
	torchvision.transforms.ToTensor(),
	torchvision.transforms.Normalize(mean=(0.4885, 0.456, 0.406), std=(0.229, 0.224, 0.225))
])
```

![[Pasted image 20261006191443.png]]


## Weight Initialization

> [!question] Question:
> - Why do we need random weight initialization ?
> - What happens if initialize all training parameters (weights) to the same-value ? Such as 0

All the neurons will **do the same thing**, **output** the **same** thing, all get the **same gradient**, **update** in the **same** way, all neurons are **exactly same**.

1. Weights should be small but not too small
2. Weights should be different

![[Pasted image 20261006191752.png]]

> [!note]
> **Activations saturate**: Means that if the weights is too big the update will be very small and might not change much


![[Pasted image 20261006191901.png]]


![[Pasted image 20261006191927.png]]
































