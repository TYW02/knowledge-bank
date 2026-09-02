---
title: Lab 1
tags:
  - Tensor
---
# Tensor Basic
- `.size()` or `.shape`
```python
print(x.size()) # They both return the same thing
print(x.shape)
xsize = tuple(x.size())

# Fetching size of specific dimension
print(x.shape[0])
print(x.size(0))
```
- **dtype**: Type of numerical elements (mainly use torch.float32)
```python
print(x.dtype)
```
- **device** it is placed on (cpu, cuda:0, cuda:1)
```python
print(x.device)
```


# Initialization
- Directly from data (list of numpy.adarray)
```python
a = torch.tensor([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
a = np.random.normal(5, size=(2, 3)).astype('float32')
x = torch.from_numpy(a) # this does NOT COPY data
```
- Tensors of constant zeros & ones & random
```python
a = torch.zeros((5, 3))
a = torch.ones(3)
a = torch.empty((64, 32, 3, 3)).fill_(32.)
c = torch.full((2, 3), 3.141592)
d = torch.randn((2, 3))
```

## Device Placement
```python
print(x.device)
b = x.to('cuda:0')
b = x.to('cpu')
```

> [!Important Knowledge]
> On Multi-GPU (and vanilla jobs) restrict yourself to 1 device, don't grab all GPUs

# Common Operations
## Change Shape (`.view` & `.reshape`)
```python
x = torch.ones((10))
y = x.view((2, 5))
z = x.view((-1, 5)) # This will be shape (2, 5)
# -1 acts as a placeholder for automatic calculation
y = x.reshape((2, 5))
```
To calculate the final dimension when using '-1' multiply the original shape to find total number of elements, then divide by the known target dimension
### Example
- Original Shape `(32, 64, 7, 7)`
- Total no. of elements: 100,352
- `.view(32, -1, 14)`
- 32 * 14 = 448
- 100,352 / 448 = 224
- Final shape: `(32, 224, 14)`

## Swap 2 dimensions (Transpose)
```python
x = torch.randn(2, 3)
print(x.shape) # (2, 3)

a = x.transpose(0, 1) # swap dim0 with dim1
print(a.shape) # (3, 2)
```

## Permute
```python
x = torch.randn(2, 3, 5)
print(torch.permute(x, (2, 0, 1)).shape) # old dim2 = dim1, old dim0 = dim1, old dim1 = dim 2
# (5, 2, 3)
```

## Squeeze: Remove Specified dimension with length = 1

`torch.squeeze(A, dim=2)` Removes Singleton dim `(a, b, 1, c) -> (a, b, c)`

```python
x = torch.zeros([1, 2, 3])
print(x.shape) # (1, 2, 3)
x = x.squeeze(0)
print(x.shape) # (2, 3)
```

`torch.unsqueeze(A, dim = 1)` Insert Singleton dim `(a, b, c) -> (a, 1, b, c)`
```python
x = torch.zeros([2, 3])
print(x.shape) # (2, 3)
x = x.unsqueeze(1)
print(x.shape) # (2, 1, 3)
```

## Cat: Concatenate multiple tensors
```python
x = torch.zeros([2, 1, 3])
y = torch.zeros([2, 3, 3])
z = torch.zeros([2, 2, 3])
w = torch.cat([x, y, z], dim=1)
w.shape # (2, 6, 3)
```

> [!IMPORTANT]
> Shapes DO NOT have to completely match BUT
> They **MUST** match on every dimension **EXCEPT** the one you are concatenating along

## Broadcasting
```python
a = torch.full(( 3), 3.)
b = torch.full((1, 3), 3.)
c = a + b # shape will be (1, 3)
```


## Vector-to-vector Dot Product
`torch.dot`
```python
# a, b MUST be 1-tensors
a.size() = b.size()
torch.dot(a, b)
```

## Matrix-to-matrix Matrix Multiplication
`torch.mm`
```python
# a, b MUST be 2-tensors
a.size() = (n, m)
b.size() = (m, p)
torch.mm(a, b) # Size: (n, p)
```


### Multiplication + broadcasting
```python
bias = torch.randn(10)
x = torch.randn(32, 784)
w = torch.randn(784, 10)

# Perform matrix multiplication and add the bias
temp = torch.mm(x, w)
print(temp.shape) # (32, 10)

print(bias.shape) # 10

y = temp + bias # this is the broadcasting part
print(y.shape) # (32, 10)
```


# PyTorch Workflow
![[Pasted image 20260902223226.png]]


## Train Phase
> Loop over minibatches of training data
1. Set model to train
2. Fetch input and ground truth tensor (X, y), move them to device
3. Compute model prediction (y_pred)
4. Compute Loss
5. Set accumulated gradients of model parameters to 0 (`optimizer.zero_grad()`)
6. Run `loss.backward()` to compute gradients of loss function with respect to parameters
7. Run optimizer (`optimizer.step()`) to apply gradients to update model parameters

## Validation Phase
> Loop over minibatches of validation data
1. Set model to evaluation mode
2. Fetch input and ground truth tensors (X, y)
3. Move them to device
4. Compute model prediction (y_pred)
5. Compute loss in minibatch
6. Compute loss average / accumulated over all minibatches
7. If averages loss is lower than the best loss so far, save the state dictionary of the model containing the model parameters
Return best model parameters


### Available libraries in PyTorch
`torchvision.models`: Pretrained models
`torchvision.dataset`: Popular datasets
`torchvision.transforms`: Transformations to preprocess datasets

Utilities to create custom datasets and dataloaders
`torch.utils.data`: Helps handle datasets and provides tools to load and preprocess data efficiently
`torch.utils.data.DataLoader()`: Wraps dataset and provides mini-batches of the data
- Batching data
- Shuffling
- Parallel loading


# Example Code
```python
import torch
import torchvision
import torchvision.transforms as transforms

torch.manual_seed(42)

batchsize=32
maxnumepochs=3

device=torch.device("cpu")

datatransforms = transforms.Compose([
	transforms.ToTensor(),
	transforms.Normalize((0.1307,), (0.3081))
	# Subtract all pixel by mean per channel and divide by std per channel
	# Makes training more stable if data is centered around 0
])
```


```python
# Map-style Dataset class
ds = {
	'trainval': datasets.FashionMNIST('./.data', train=True, download=True, transform=datatransforms),
	'test': datasets.FashionMNIST('./data', train=False, download=True, transform=datatransforms)
}
```

| Map-Style                                                                                                 | Iterable-Style                                                               |
| --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Provides datasample by asking for i-th data point                                                         | Provides data sample using python iterator                                   |
| Suitable for **static data** with fixed dataset size e.g. benchmark dataset, image on disk (index access) | Suitable for streaming or otherwise dynamic data sources (Sequential access) |
```python
class ds(torch.utils.DataSet):
	def __init__(self, ...):
		super().__init__()
		# Store transforms as class member, so it can be used in getitem
		pass
		
	def __len__(self):
		# returns number of sample in dataset
		pass
		
	def __getitem__(self, i):
		# return i-th sample and its label, and additional data
		# does all processing (load, transform, resize)
		pass
```


# Creating DataLoader
Usually shuffle=True for training set, but here we are using SubsetRandomSampler
```python
dataloaders={
	'train': torch.utils.data.DataLoader(ds['trainval'],
	batch_size=batchsize, shuffle=False, sampler=torch.utils.data.sampler.SubsetRandomSampler(np.arange(50000))
	),
	'val': torch.utils.data.DataLoader(ds['trainval'],
	batch_size=batchsize, shuffle=False, sampler=torch.utils.data.sampler.SubsetRandomSampler(np.arange(50000, 60000))
	),
	'test': torch.utils.data.DataLoader(ds['test'],
	batch_size=batchsize, shuffle=False
	)
}
```

# Define Prediction Model
```python
numcl = 10
indims = 784
batchsize=32
model = onelinear(indims, numcl).to(device)
```

![[Pasted image 20260902225551.png]]

## Define Loss
```python
numcl = 10
indims = 784
batchsize=32
model = onelinear(indims, numcl).to(device)

loss = torch.nn.CrossEntropyLoss(weight=None, size_average=None, ignore_index=-100, reduce=None, reduction='mean')
```
> [!CAREFUL]
> `nn.CrossEntropyLoss` applies `nn.LogSoftmax` + `nn.NLLLoss`(Negative log likelihood loss)
> So there is no need to apply softmax in last layer

## Define Optimizer
```python
lrates = [0.01, 0.001]

best_hyperparameter = None
weights_chosen = None
bestmeasure = None

for lr in lrates:
	print('\n\n\n###NEW RUN###')
	optimizer = optim.SGD(model.parameters(), lr=lr, momentum=0.9)
```
> Optimizer: Applies the computed gradients to change the trainable parameters of the model. 

## Loop over epoch
```python
for lr in lrates:
	best_epoch, best_perfmeasure, bestweights = train_modelcv(dataloader_cvtrain = dataloaders['train'], dataloader_cvtest =  dataloaders['val'], model = model, criterion = loss, optimizer = optimizer, scheduler = None, num_epochs = maxnumepochs, device = device)
	
	if best_hyperparameter is None:
		best_hyperparameter = lr
		weight_chosen = bestweights
		bestmeasure = best_perfmeasure
	elif best_perfmeasure > bestmeasure:
		best_hyperparameter = lr
		weights_chosen = bestweights
		bestmeasure = best_perfmeasure
```

## Test Phase
```python
model.load_state_dict(weights_chosen)

accuracy, _ = evaluate(model=model, dataloader=dataloaders['test'], criterion=None, device=device)

print('accuracy val', bestmeasure.item(), 'accuracy test', accuracy.item())
```


# Deep Dive into training code
```python
def train_modelcv(dataloader_cvtrain, dataloader_cvtest, model, criterion, optimizer, scheduler, num_epochs, device):
	best_measure=0
	best_epoch = -1
	for epoch in range(num_epochs):
		losses=train_epoch(model, dataloader_cvtrain, criterion, device, optimizer)
		measure, _ = evaluate(model, dataloader_cvtest, criterion=None, device=device)
		print(' perfmeasure', measure.item())
		if measure > best_measure:
			bestweights = model.state_dict()
			best_measure = measure
			best_epoch = epoch
			print('current best', measure.item(), ' at epoch ', best_epoch)
	return best_epoch, best_measure, bestweights
```

```python
def train_epoch(model, trainloader, criterion, device, optimizer):
	model.train()
	losses = []
	for batch_idx, data in enumerate(trainloader):
		inputs=data[0].to(device)
		labels=data[1].to(device)
		
		outputs = model(inputs)
		loss = criterion(outputs, labels)
		
		losses.append(loss.item())
		
		optimizer.zero_grad()
		loss.backward()
		optimizer.step()
		
	return losses
```

```python
def evaluate(model, dataloader, criterion, device):
	model.eval()
	with torch.no_grad():
		datasize=0
		accuracy=0
		avgloss=0
		for ctr, data in enumerate(dataloader):
			inputs = data[0].to(device)
			outputs = model(inputs)
			labels = data[1]
			cpuout = outputs.to('cpu')
			if criterion is not None:
				curloss = criterion(cpuout, labels)
				avgloss = (avgloss*datasize + curloss) / (datasize + inputs.shape[0])
				
			labels = labels.float()
			_, pred = torch.max(cpuout, 1)
			accuracy = (accuracy*datasize + torch.sum(preds == labels) / (datasize + inputs.shape[0]))
			datasize += inputs.shape[0]
			
	if criterion is None:
		avgloss = None
		
	return accuracy, avgloss
```

```python
class onelinear(nn.Module):
	def __init__(self, dims, numout):
		super().__init__()
		self.bias = torch.nn.Parameter(data=torch.zeros(numout), requires_grad=True)
		self.w = torch.nn.Parameter(data=torch.randn((dims, numout), requires_grad=True))
		
	def forward(self, x):
		v = x.view((-1, 28*28)) # Flatten image
		y = self.bias + torch.mm(v, self.w)
		return y
```















