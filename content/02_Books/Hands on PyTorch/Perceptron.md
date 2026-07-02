---
title: Perceptron
tags:
  - Perceptron
---
#Perceptron  is the simplest building block in neural networks.
> [Perceptron](https://www.geeksforgeeks.org/deep-learning/what-is-perceptron-the-simplest-artificial-neural-network/)

We start by creating the Perceptron class and defining the parameters
>[!Example]-
>```python
>def __init__(self, eta = 0.01, n_iter = 50, random_state = 1):
>	self.eta = eta
>	self.n_iter = n_iter
>	self.random_state = random_state
>```

We also create other functions that help the model:

### Calculating the prediction
> [!Code Block]-
> ```python
> def net_input(self, X):
> 	return np.dot(X, self.w_) + self.b_
> ```


### Comparing Prediction to Target
> [!Code Block]-
> ```python
> def predict(self, X):
> 	return np.where(self.net_input(X) >= 0.0, 1, 0)
> ```


## Fit function
> [!Code Block]-
> ```python
> def fit(self, X, y):
> 	rgen = np.random.RandomState(self.random_state)
> 	self.w_ = rgen.normal(loc = 0.0, scale = 0.01, size = X.shape[1])
> 	self.b_ = np.float_(0.)
> 	self.errors_ = []
> 	
> 	for _ in range(self.n_iter):
> 		errors = 0
> 		for xi, target in zip(X, y):
> 			update = self.eta * (target - self.predict(xi))
> 			self.w_ += update * xi
> 			self.b_ += update
> 			errors += int(update != 0.0)
> 		self.errors_.append(errors)
> 	return self
> ```


# How to use the class
> [!Code Block]-
> ```python
> ppn = Perceptron(eta = 0.1, n_iter = 10)
> ppn.fit(X, y)
> plt.plot(range(1, len(ppn.errors_) + 1), ppn.errors_, markers = 'o')
> plt.xlabel('Epochs')
> plt.ylabel('Number of updates')
> plt.show()
> ```

