---
title: Convolutional Neural Network
tags:
  - CNN
---

# Why do we need CNNs?
A fully connected network treats every input pixel independently.

This is very wasteful because:
- Nearby pixels are strongly related.
- Objects can appear anywhere in the image
- Fully connected layers have huge number of parameters

CNN looks at **local patches** of the image by using a small sliding window called a *kernel* or *filter*
- Instead of connected every pixel to every neuron, every neuron only looks at a small region.

2 properties of CNN:
1. Local Connectivity: Patterns are detected in small neighborhoods
2. Weight sharing: The same kernel is used across the whole image. (A kernel of 3x3 will only need 9 weights for the whole Conv layer)

## Convolution Operation
A convolution is a sliding window operation

At each position:
1. Take a patch of the input the same size as the kernel
2. Multiply each input value by the corresponding kernel value
3. Add all the results together
4. That sum becomes 1 output value

Input $X$ of shape $3$ x $3$:
$X = \begin{bmatrix}1&2&3\\4&5&6\\7&8&9\end{bmatrix}$

Kernel $K$ of shape $2$ x $2$:
$K = \begin{bmatrix}1&0\\0&-1\end{bmatrix}$

Stride 1, no padding, Output Size:
$\frac{3-2}{1} + 1 = 2$
So the output is $2$ x $2$

### First Output Position
Top-left patch:
$\begin{bmatrix}1&2\\4&5\end{bmatrix}$

Multiply element-wise:
$(1 \cdot 1) + (2 \cdot 0) + (4 \cdot 0) + (5 \cdot -1)$ = $1 + 0 + 0 -5 = -4$
So the top-left output value is -4

If you repeat this for the other positions, this particular kernel and input produces:
$\begin{bmatrix}-4&-4\\-4&-4\end{bmatrix}$
In a real CNN, the kernel values are the **learned weights**

## Output Size Formula
Given:
- Input Size $N$
- Kernel Size $K$
- Padding $P$
- Stride $S$

The output size is:
$out = \lfloor\frac{N - K + 2P}{S}\rfloor + 1$

Example:
For FashionMNIST, each image is $28$ x $28$
If we use a $3$ x $3$ kernel, stride 1, padding 1:
$out = \lfloor\frac{28 - 3 + 2 \cdot 1}{1}\rfloor + 1 = 28$
Padding of 1 preserves the spatial size

## Padding
Padding adds extra border values, usually zeros, around the input

Use Case:
- Without padding, the output shrinks after each convolution.
- Padding helps preserve spatial dimensions.
- Gives kernel access to edge pixels more often.

For add-sized kernel, same padding with stride 1 means:
$P = \frac{K - 1}{2}$

So for a $3$ x $3$ kernel: $P = 1$
For a $5$ x $5$ kernel: $P = 2$

## Stride
Controls how far the kernel moves each step
- Stride 1: Kernel moves 1 pixel at a time
- Stride 2: Kernel jumps 2 pixel at a time

Larger Stride:
- Reduces output size
- Reduces Computation
- Can make model more efficient

> [!What If Stride Is Large ?]
If stride is too large, kernel may skip important details


## Channels and Feature Maps
Black-and-white image has 1 channel
An RGB image has 3 channels: $shape = 3$ x $H$ x $W$

A convolutional layer with $C_{out}$ filters produces $C_{out}$ output channels
Each output channel is called a **feature map**

For each output channel, there is 1 filter/kernel
For an input with $C_{in}$ channels and kernel size $K$, each filter has shape:
$C_{in}$ x $K$ x $K$
The convolution sums over all input channels.


## Parameter Counts for a Conv Layer
For a convolutional layer:
$parameters = (C_{in}$ x $K$ x $K + 1)$ x $C_{out}$
The +1 accounts for the bias

Example:
Input has 3 channels, kernel $3$ x $3$, output has 16 channels
$(3 \cdot 3 \cdot 3 + 1) \cdot 16 = (27 + 1) \cdot 16 = 448$
A fully connected layer from a 32 x 32 x 3 image with 16 neurons would have:
$(32 \cdot 32 \cdot 3 + 1) \cdot 16 = 3073 \cdot 16 = 49168$

CNNs are much more parameter-efficient

## Pooling
Reduces the spatial size of feature maps.
The most common type is max pooling

Max Pooling:
1. Take a small window, often 2 x 2
2. Keep the largest value in that window
3. Slide the window by the pool size

Example:
Input = $\begin{bmatrix}1&2\\3&4\end{bmatrix}$

Max pooling with a 2 x 2 window: $max(1,2,3,4) = 4$

So the output is a single value: 4.

> [! Why use Pooling ?]
> - Reduces spatial size, which reduces computation.
> - Makes the model slightly more robust to small translations.
> - Increases the receptive field of later layers. (When later layers looks at this compressed values they can see a much wider field of the original image)

## Typical CNN Block
A standard CNN is built from repeated blocks:
$Conv2d -> ReLU -> MaxPool2d$

After several blocks: $Flatten -> Linear -> ReLU -> Linear$
The convolutional layers learn spatial features.
The full connected layers perform classification using those features

> [!Important]
> `nn.CrossEntropyLoss` is PyTorch expects raw logits, so we do **NOT** add softmax to the model.

