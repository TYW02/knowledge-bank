---
title: W3 CNN
---


# MLP Limitations
> Image data is represented as a 2D grid of pixels regardless of color channels

## Problem
> A Fully Connected MLP does not take into account of the spatial relation between pixels & don't scale well to images of larger size

## Solution
> Convolution Neural Network are designed precisely for this purpose


# 1D data & 1D Convolutions

> 1D sequence data such as audio

- N: Batch Size
- \# channels: features measured in parallel at each time index (Mono audio waveform with 1 channel, Stereo audio L/R with 2 channels)
- L: Sequence length

## Convolution
> Combines 2 sequences of signal to see how much 1 "overlaps" with a shifted, flipped version of the other

- Slide **learned kernels** over data with weight
- Mathematically, convolution slides a flipped kernel, but cross-correlation slides the kernel as it is
- 1D convolutions: conv along **1 direction**

> [!Key Idea]
> Neighbor pixels tend to be related, so we connect only neighboring neurons in the input

```python
input = torch.tensor([1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0])
input = input.reshape(1, 9)

m = nn.Linear(9, 5)
output = m(input)
print(output.size()) # (1, 9) @ (9, 5) = (1, 5)
```


## 1D Convolution - 1 input channel

### Convolution
Compute inner products between an input tensor and a **kernel** tensor $w$ along a **sliding window** moving along the input

![[Pasted image 20260914191035.png]]

```python
input = torch.tensor([1.0, 2.0, 3.0, 8.0, 5.0, 6.0, 7.0, 8.0, 9.0])
batch_size, num_channels, length = 1, 1, 9
input = input.reshape(batch_size, num_channels, length)

m = nn.Conv1d(in_channels=1, out_channels=1, kernel_size=3, stride=1, bias=False)
m.weight = nn.Parameter(torch.tensor([[[2.0, 5.0, 3.0]]])) # Shape: (1, 1, 3)

output = m(input)
print("Output:\n", output)
```

# 1D Convolution - More Input Channels
![[Pasted image 20260914191537.png]]


```python
input = torch.tensor([[1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0],
					[7.0, 5.0, 1.0, 0.0, 6.0, 8.0, 2.0, 10.0, 3.0],
					[2.0, 3.0, 5.0, 6.0, 0.0, -9.0, 1.0, 7.0, 12.0],
					[7.0, 5.0, 1.0, 0.0, 6.0, 8.0, 2.0, 6.0, -5.0]
])

batch_size, num_channels, length = 1, 4, 9
input = input.reshape(batch_size, num_channels, length)
m = nn.Conv1d(in_channels=4, out_channels=1, kernel_size=3, stride=1, bias=False)
m.weight = nn.Parameter(torch.tensor([[[2.0, 5.0, 3.0], [6.0, 1.0, 2.0], [-5.0, 0.0, 7,0], [6.0, 9.0, 3.0]]]))
output = m(input)
print(output.shape) # (1, 1, 7)
```

> [!Output Calculation]
> Output Length = $\lfloor \frac{InputLength - KernelSize}{Stride} \rfloor + 1$
> Input length - Kernel Size = $9 - 3$
> Divide by the stride = $6/1 = 6$
> Add 1 = $6 + 1$

^8e885f


# 1D Convolution - More Output Channels
![[Pasted image 20260914193332.png]]

- More output channels = more potential patterns to learn

# 2D data & 2D Convolution
- N: Batch size
- \# channels: 3 for RGB image
- 2D dim: Height, Width
- 2D Convolution: Conv slide along 2 directions

![[Pasted image 20260914194004.png]]

> [!Note]
> The resulting output created is the `feature map`
> 
> Since CNN use shared weights, we have lesser training parameters in this case '4' or '5' if you count the bias


![[Pasted image 20260914194209.png]]

```python
input = torch.arange(35)
batch_size, num_channels, width, height = 1, 1, 5, 7
input = input.reshape(batch_size, num_channels, width, height).float()

m = nn.Conv2d(in_channels=1, out_channels=1, kernel_size=3, stride=1, bias=False)
output = m(input)
print(output.shape) # (1, 1, 3, 5)
```

> [!Output Calculation]
> Here just use the same formula as [[W3 CNN#^8e885f|Formula]]
> 
> But you calculate height and width separately
> Height = (5-3) / 1 + 1 = 3
> Width = (7-3) / 1 + 1 = 5

![[Pasted image 20260914194840.png]]

> [!Note]
> Here we say stride determine granularity of the feature map because stride allows us to 'skip' pixels and by doing so we create a smaller feature map and also skip over some of the features


## 2D Convolution - More input channels
![[Pasted image 20260914195005.png]]


## 2D Convolution - More output channels
![[Pasted image 20260914195055.png]]

- By having more output channels we can capture more patterns 

> [!Parameter Formula]
> ((Kernel Size \* Input Channel) + 1) \* Output Channel
> - TAKE NOTE +1 IS BIAS
> - Example:
> 	- (2 \* 2 \* 2) \* 2 = 16
> 


# Why Convolutions ? - Less Parameters
- Fully Connected layers: Each neuron of the layer is connected to each of the next neuron
![[Pasted image 20260914195904.png]]

## Compared to CNN
- 1D conv with kernel size 5: The total parameter is 5 **no matter** how many inputs or outputs are in the sliding dimension


# Convolution Layer are pattern detectors
- A kernel is a **template/matched filter**, at each location, it computes $y = mx + b$
- After **non-linearity** a strong positive response can be seen as "Pattern found"
- **Weight/kernel sharing**: The same detector slides everywhere, so there is no need to relearn the same pattern at each position

> [!Note]
> Convolutions is **translation-invariant** (Spatial shift)
> 
> HOWEVER, Standard CNNs are **NOT** rotation or scale invariant by default

![[Pasted image 20260914222101.png]]


# Pooling (Downsamping)

## Max Pooling
- Computes max of all the elements over a window and returns a real number

## Average Pooling
- Compute average over the elements in the window

> [!Main Idea]
> Pooling layers are usually used after convolution + activation layers, to reduce the spatial dimensions and add local translation invariance

![[Pasted image 20260914222304.png]]

# Padding
![[Pasted image 20260914222319.png]]

- Add for EVERY dimension at both ends of an input a layer of ZEROS

> [!Why]
> - Preserve the height and weight to design deeper network
> - Improves performance by keeping information at the boarders


# Theoretical Receptive Field
- Receptive Field: Size of the region in the INPUT that produces the feature
- For convolution with kernel size K, each element in the output depends on a $K * K$ receptive field in the input
![[Pasted image 20260914222605.png]]

> [!Note]
> This is why the lower layers of a CNN learns "Low-level features" since the kernels are looking at a "**Smaller**" portion of the image.
> 
> While **deeper** layers are looking at "More" pixels they can represent more **abstract** features.
> 

![[Pasted image 20260914222811.png]]

> $Receptive_{Prev} + (Kernel - 1) * (Stride_{i})$
> Take the previous receptive field + (Kernel size - 1) * (Stride from i = 0 to current)

> [!Note]
> By stacking convolution layers we can look at regions that get larger with every layer.
> - If you stack 2 layer of 3x3 kernel, 
> 	- 1st layer looks at 3x3
> 	- 2nd looks at 5x5
> - Each layer looks at regions in the input image with a larger size
> - Better stack simple functions in many layers than learning in 1 layer something very complex


# Dilated Convolutions
- Dilated convolutions: Operation with different degrees of spacing between the elements of the feature map
- Obtain larger receptive fields, looks at larger context without increasing the number of parameters
![[Pasted image 20260914223730.png]]



#### References
- https://d2l.ai/chapter_convolutional-neural-networks/index.html  
- https://cs231n.github.io/convolutional-networks/  
#### Beautiful CNN visualizations:  
- https://alexlenail.me/NN-SVG/
- https://adamharley.com/nn_vis/  
- https://deeplizard.com/resource/pavq7noze2  
- https://github.com/vdumoulin/conv_arithmetic  












