
```python
def train_epoch(model, trainloader, criterion, device, optimizer):
    model.train()  # IMPORTANT: training mode
    losses = []
    for batch_idx, data in enumerate(trainloader):
        inputs = data[0].to(device)
        labels = data[1].to(device)
        outputs = model(inputs)
        loss = criterion(outputs, labels)
        optimizer.zero_grad()  # reset accumulated gradients
        loss.backward()        # compute new gradients
        optimizer.step()       # apply gradients
    return losses
```

> [!important] What it does
> One full pass over the training data.
> - `model.train()` enables dropout / batchnorm training behavior.
> - `zero_grad()` clears old gradients
> - `backward()` computes gradients
> - `step()` updates weights

> [!debug] If you change
> - Removing `zero_grad()` **accumulates** gradients across batches
> - Removing `model.train()` may cause dropout / batchnorm to **behave incorrectly**


# Evaluation Loop
```python
def evaluate(model, dataloader, criterion, device):
    model.eval()  # IMPORTANT: eval mode
    with torch.no_grad():  # do not record computations for gradient
        datasize = 0
        accuracy = 0
        avgloss = 0
        for ctr, data in enumerate(dataloader):
            inputs = data[0].to(device)
            outputs = model(inputs)
            labels = data[1]
            cpuout = outputs.to('cpu')
            if criterion is not None:
                curloss = criterion(cpuout, labels)
                avgloss = (avgloss * datasize + curloss) / (datasize + inputs.shape[0])
            labels = labels.float()
            _, preds = torch.max(cpuout, 1)
            accuracy = (accuracy * datasize + torch.sum(preds == labels)) / (datasize + inputs.shape[0])
            datasize += inputs.shape[0]
            if criterion is None:
                avgloss = None
    return accuracy, avgloss
```

> [!important] What it does
> Evaluates model on validation/test data
> - `model.eval()` disables dropout/batchnorm training behavior.
> - `torch.no_grad()` saves memory and computation
> - Accuracy is running average


> [!debug] If you change
> **Removing** `model.eval()` gives **wrong predictions** if **dropout/batchnorm exists**
> **Removing** `torch.no_grad()` **increases** memory usage.



# Basic Augmentation Transforms
```python
train_augmented_transforms = transforms.Compose([
    transforms.Resize((36, 36)),
    transforms.RandomCrop((32, 32)),
    transforms.ColorJitter(brightness=0.5),
    transforms.RandomRotation(45),
    transforms.RandomHorizontalFlip(p=0.5),
    transforms.RandomGrayscale(p=0.2),
    transforms.ToTensor(),
    transforms.Normalize(mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225)),
])

test_transforms = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize(mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225))
])
```

> [!debug] If you change
> - `Resize((36,36))` → different size **changes input resolution**. 
> - `RandomCrop((32,32))` → different crop size **changes output size**.
> - `ColorJitter(brightness=0.5)` → larger values = **more color variation**.
> - `RandomRotation(45)` → larger angle = **more rotation variation**.
> - `RandomHorizontalFlip(p=0.5)` → `p=0.3` flips **less often**.
> - `RandomGrayscale(p=0.2)` → `p=0.5` converts to grayscale **more often**.
> - `Normalize` mean/std → different values **change input distribution**.


# Fine-Tuning / Transfer Learning
```python
# Load pretrained model
model = torchvision.models.resnet50(pretrained=True)

# Replace last layer
num_ftrs = model.fc.in_features
model.fc = torch.nn.Linear(num_ftrs, 102)  # 102 flowers

# Train
optimizer = optim.SGD(model.parameters(), lr=0.001, momentum=0.9)
```

> [!important] What it does
> **Loads** ImageNet-pretrained weights, **replaces** final layer for new task, fine-tunes

> [!debug] If you change
> - `pretrained=True` -> `False` trains from scratch (worse for small data)
> - `model.fc` -> different layer name for different architecture
> - `102` -> number of classes in your dataset
> - `lr=0.001` -> smaller learning rate for fine-tuning 

### Why Bottom Layers are Reusable
- Low-level features (edges, textures) learned on ImageNet **generalize to many tasks**. More **specific features are in higher layers**


# Overfitting vs Underfitting

| Symptom                            | Fix                                                       |
| ---------------------------------- | --------------------------------------------------------- |
| Huge train / val gap (Overfitting) | Increase regularization, get more data, reduce model size |
| No gap, both low (Underfitting)    | Train longer, bigger model, check optimization            |

> [!important] If you change
> - Reduce **Overfitting**: Add `dropout`, `weight decay`, **data augmentation**
> - Reduce **Underfitting**: Increase **model capacity**, Increase **training time**







































