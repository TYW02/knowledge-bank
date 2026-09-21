---
title: W4 CNN Architecture
---
# LeNet

- Convolution - Activation - Pooling repeated
- The Last layers are fully connected

![[Pasted image 20260921213447.png]]

![[Pasted image 20260921213456.png]]



# AlexNet: Trial and Error
- ReLU for all layers except final layer (Softmax)
- Normalization
- Overlapping pooling
- Image Augmentation
	- Image translation & Horizontal Reflection
	- Alter RGB intensity
- Dropout
![[Pasted image 20260921213609.png]]


## Dropout
- Randomly drop node (Along with their connections) during training. Typically **disable dropout** at **test time**
- Each node is retained with a fixed dropout rate $p$, independent of other nodes
- Typical choices: 20% of input nodes, 50% of hidden nodes

![[Dropout#How does Dropout work]]![[Dropout#Why we use it]]
![[Pasted image 20260921214625.png]]

- Injecting noise by setting features to 0 reduces the statistical correlation between features
	- Model cannot overfocus on a few correlations which are support well by the training data
	- Instead, it has to rely on a mixture of several different correlations between features


# Key Factors in architecture design
![[Pasted image 20260921214754.png]]

## Convolution Layers
- Takes up the most memory usage
- Most FLoating-point Ops occur 
## Fully-Connected Layers
- **Nearly all** parameters are in FC layer


# VGG: Deeper but Regular
![[Pasted image 20260921214928.png]]

- 6 different architecture
- **5 Conv** block followed by **3 fully connected**
- ALL **conv** are **3x3** stride 1 pad 1
- ALL **max pool** are **2x2** stride 2
- **After** pool, **at least double** the number of output channels

![[Pasted image 20260921215059.png]]



## Batch Normalization
- Deep NN is hard to train
	- Distribution of inputs for each layer over the process of training might be bad for optimization
- **Idea**: "Normalize" the outputs of a layer so they have zero mean and unit variance
	- Help reduce "internal covariate shift" improves optimization
	- Stabilize or accelerate the optimization process of NN

![[Pasted image 20260921215848.png]]

![[Pasted image 20260921215859.png]]

> [!Warning]
> Better not to use if your batch size is small


# ResNet: Go Deep with "Residuals"
- Found that deeper model DO NOT have better training errors
- Hypothesis: This is an **optimization problem**, deeper models are harder to optimize
	- Deeper model should be able to **perform at least as well as** the shallower model
- Solution: Change the network so learning **identity functions** with extra layers is easy

![[Pasted image 20260921220155.png]]


![[ResNet#Characteristics]]




# Visualize output of conv layers
![[Pasted image 20260921222254.png]]

> [!Note]
> You are looking at the **feature maps** (Activation maps)
> 
> Feature map is the **output values produced** when a specific filter slides across an input image or previous layer's output


## Last layer as feature embeddings
- Use L2 nearest neighbors in feature space to identify similar images
- Forward pass all image through trained CNN, extract features from FC layer prior to classifier head and compare the L2 distances to look for similarity

> [!Caution]
> Use the layer before the softmax (Classifier) Layer

![[Pasted image 20260921222549.png]]


- The last layer is a large dimension vector
- Beyond 3 dimensions is difficult to visualize and typically 2D plots are easy to comprehend
- The higher dimension to 2/3D reduction typically done using
	- Principle Component Analysis (PCA)
	- t-SNE (t-distributed Stochastic Neighbor Embedding)


## Maximally Activating Patches
> Take a large dataset of images, feed them through the network and keep track of which image patches maximally activate some neuron

1. Pick a layer and channel. The channel could be selected by finding maximal activations
2. Run many images through the network, record values of chosen channel (Use forward hook)
3. Visualize image patches (Receptive Field) that correspond to maximal activation number

![[Pasted image 20260921222919.png]]


## Saliency via Occlusion
1. Mask regions in the images (Slide the mask) each time predicting the class
2. Identify the regions which will miss classify the most 

![[Pasted image 20260921223006.png]]




























