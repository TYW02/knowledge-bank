

## Max Pool VS Avg Pool
| Feature   | Max Pooling              | Average Pooling       |
| --------- | ------------------------ | --------------------- |
| Operation | Selects Maximum Value    | Calculates Mean Value |
| Detail    | Preserves sharp features | Smooths feature map   |
| Purpose   | Highlight textures       | Reduce noise levels   |

## Channels in Pooling VS Convolution
| Feature     | Pooling                | Convolution               |
| ----------- | ---------------------- | ------------------------- |
| Processing  | Each channel separate  | Channels usually combined |
| Output size | Same as input channels | Variable                  |
| Weights     | None (Fixed function)  | Learned kernel weights    |

# Pooling in Computer Vision

> [!important] What Pooling Does
> Pooling is a **downsampling** operation. It slides a window over the input and **reduces each window to a single value**.
> - **NO** learnable parameters

## Why Pooling Exists

### 1. Reduce Spatial Dimensions
Fewer computations and parameters in later layers
### 2. Increase Receptive Field
Each later neuron sees a larger input region (Stride multiplies the jump)
### 3. Provide Translation Invariance
Small shifts in the input produce the same pooled output
### 4. Summarize local features
Keeps the strongest (max) or average response in each region
### 5. Control Overfitting
Coarser representations reduce the model's ability to memorize exact pixel positions.



# Types of Pooling

## Max Pooling
Takes the maximum value in each window
```python
Input window:      Max pool 2×2, stride 2:
[1  3]             
[2  4]             → 4
```
- Keeps the **strongest** activation
- Most common in classification CNNs ( #Alexnet, #TinyVGG , #ResNet)
- Preserves **sharp** features (edges, corners) that survive into deeper layers
- Gradient flows **only** through the **max element** 

## Average Pooling
Takes the mean of each window
```python
Input window:      Avg pool 2×2, stride 2:
[1  3]
[2  4]             → (1+2+3+4)/4 = 2.5
```
- Smooths the output
- Used in some architecture ( #LeNet, older networks )
- Gradients flows through all elements equally
- Less common in modern classification, more common near the output

# How Pooling Affects the Model

## Receptive Field
Pooling with stride `s` multiplies the running jump

- A MaxPool2x2 s2 after a Conv3x3 s1:
	- RF before: 3
	- RF after: 3 + 1 * 1 = 4
	- Multiplier after: 2 (affects all subsequent layers)

## Translation Invariance

Pooling gives **local translation invariance**. If the input **shifts by 1 pixel**, most pooled windows **produce the same output**. 

> This is why CNNs can recognize a "cat" whether it's top-left or bottom-right

## Gradient Flow
- Max Pool: Gradient **flows only** through the **max element**. Acts like a **switch** that routes **gradient to the strongest activation**
- Avg Pool: Gradient **distributes evenly** (1/($k^2$) per element). **Smooths gradients**

## Parameter Count
Pooling has **zero learnable parameters**. It's pure compute

> [!warning] PyTorch 
> ```python
> nn.MaxPool2d(3)
> # This will set BOTH kernel_size and stride = 3
> ```


# Summary
- Pooling **reduces spatial dimensions**, **grows** the **receptive field**, and provides **translation invariance** with zero parameters. 
- **Max pool** keeps the **strongest response** (good for classification), **avg pool smooths** (good for texture/audio)