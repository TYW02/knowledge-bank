---
title: W8 Image Level Vision
---
<iframe src="/static/quiz/cvdl_w8_practice.html" width="100%" height="750px" style="border: 1px solid var(--lightgray); border-radius: 8px;"></iframe>
# Overview

## 1. What does the model receive ?
- Understand images and pre-processing

## 2. How do pixels become evidence ?
- CNNs VS ViTs

## 3. Which pixels drove the decision ?
- CAM and Grad-CAM

> [!important] Before Deployment
> Before you push your model to production, you should know what your model takes in and how different inputs can lead to different outcomes ?


# "What does the computer vision model actually see ?"

## Images are a Spatial distribution of numbers
- Colours, "objects", brightness -> all structure we impose on a grid
- H, W: rows, columns of pixels
- C: Channels 1(gray) or 3 (RGB or equivalent)
- dtype uint8: Integers from \[0, 255\]

![[Pasted image 20261019212234.png]]

![[Pasted image 20261019212253.png]]


# Examples of Leaks in Real Datasets
![[Pasted image 20261019212449.png]]


# Augmentation = free, label-preserving data
![[Pasted image 20261019212524.png]]


## However,
![[Pasted image 20261019212553.png]]

> [!warning] My Notes
> - **Augmentation Limitation**
> 
> Augmentation can help with overfitting BUT, if the main problem is the data, augmentation will not help.

# Three Data Checks Before Model Training

> [!information] Write the annotation guide first
> - Is a van a car ?
> - What about an occluded wolf ?
> - Decide edge cases **before** labelling, then measure inter-annotator agreement.

> [!information] Check the class balance
> 95% class A, 5% class B
> - Always answering "A" scores 95% accuracy and 0% recall on B.
> - Report per-class recall / F1

> [!information] Hunt for data leaks
> What else differs between the classes ?
> - Background, hospital, watermark, date, the snow.
> - Is this check failing ?


# "How do pixels become evidence ?"

> A Learned Filter is Weights + Bias + ReLU

![[Pasted image 20261019213503.png]]

> [!warning] Channels
> One channels **per** pattern.
> - Each output channel says, "How much of my pattern is **here**"

# Feature Hierarchy in CNNs
![[Pasted image 20261019213742.png]]

> [!warning] My Notes
> The network **activates the most** where the box is.
> - The layer on the right is the pattern the model sees.


# Embeddings: Pool Each Map Into One Number

## Global Average Pooling (GAP)

> 2D feature space is compressed to vectors showing "How much of each pattern" is kept

## Embeddings turn "Similarity" into Distance

- Near vectors = Images the model considers alike.
- The layer decides what "alike" means

![[Pasted image 20261019215022.png]]


![[Pasted image 20261019215637.png]]

![[Pasted image 20261019215706.png]]


# Vision Transformer

### CNN are inherently local
- Receptive field can be increased, but very deep CNN

### CNNs have inductive bias
- Assumption that the local pixels are "more" similar

![[Pasted image 20261019220003.png]]


# A ViT cuts the same Photo Into Patches

> No convolutions, but tokens, a learned position for each, and a \[CLS\] token that collects the answer.

![[Pasted image 20261019220354.png]]

> [!information] ViT Architecture
> ViT-B/16: (224x224 image divided into 16x16 patches) = 14x14 -> 196 patches + \[CLS\]
> - 768-d token features (Flattened 16x16x3 RGB patch)
> - 12 encoder blocks x 12 attention heads per block


# Attention by Hand: What \[CLS\] Reads
$$
Score = softmax(\frac{query \cdot key}{\sqrt{d}})
$$
![[Pasted image 20261019220534.png]]


# CNN vs ViT

|                       | CNN                                                     | ViT                                           |
| --------------------- | ------------------------------------------------------- | --------------------------------------------- |
| Built-in assumptions  | Strong (Locality, equivariance)                         | Weak (learns them)                            |
| Receptive Field       | Grows w/ depth (edges -> textures -> parts -> concepts) | Global from Layer 1                           |
| Data Requirement      | Learns from modest data                                 | Data-hungry (needs large data or pretraining) |
| Compute on big images | Scales well (Local)                                     | Attention is O ($tokens^{2}$)                 |
| Best When             | Limited data, edge deployment                           | Lots of data / pretrained                     |


# Which pixels drove the decision ?

![[Pasted image 20261019221059.png]]

## Look at the Filters (Learned Kernels)

1. Edges at every angle, color blobs, simple textures: The **vocabulary** of layer 1
2. They are the **same** for heads A and B, and for every photo. They say that the network **can** detect
3. Deeper filters (3x3x256) can't be shown as pictures at all.

![[Pasted image 20261019221311.png]]

> [!fail] Failure
> Fails: No decision in sight


## Find what one unit likes (Max Activation Patches)

> [!information] Max-Activating Patches
> Run **many photos**, keep the **crops that excite** one unit most.

![[Pasted image 20261019221517.png]]

1. Pick a **layer** and a channel* (e.g. 10th channel in model.layer4\[2\].conv3 in ResNet-101)
2. Run many images through the network, **record values of chosen channel** (Use forward hook)
3. Visualize image patches that correspond to maximal activations

> [!fail]
> Shows what a unit likes, not why this photo got "Wolf"


## Saliency via Occlusion

> [!information] Occulusion
> No gradients, no access to the weights.
> - **Just forward passes**

1. Mask regions in the images (Slide the mask) each time predicting the class
2. Identify the regions which will misclassify the most (fourth and fifth columns in the figure)

![[Pasted image 20261019222028.png]]

> If hiding a region greatly reduces the dog score, that region was important to the model's decision.

> [!Fail]
> One patch at a time **can't hide evidence** that is everywhere


![[Pasted image 20261019222235.png]]


## Saliency via Backpropagation

> Which pixels would change the score most if perturbed ?
> - One backward pass

![[Pasted image 20261019222327.png]]

1. Compute (logit(wolf) / pixel) for all 150,528 inputs (assuming 224x224x3), keep the largest magnitude per pixel
2. Large intensity **everywhere**, but **more on the snow at the bottom**
3. A gradient is **local**, it says what a tiny change would do, not what the model used.

> [!fail]
> Fast, but noisy and pixel-level


## Class Activation Map (CAM)

> [!information] Class Activation Map
> The head's weights, painted back onto the maps it pooled.

![[Pasted image 20261019222840.png]]

- CAM requires a **Global Average Pooling** (GAP) + **Linear head** (else retraining is required)
- However, only **forward pass** is required and **no backward pass**

![[Pasted image 20261019223024.png]]


# Gradient-weighted Class Activation Mapping (Grad-CAM)

> Replace the weight by the average gradient.
> - Works on **any architecture** and **any layer** (**NO GAP** needed)

![[Pasted image 20261019223207.png]]

1. Backpropagate from the target class score only (one-hot)
2. Run backpropagation till the desired convolutional layer to get the gradients at the layer (Using backward hooks) and forward propagation till the desired convolutional layer to get the activations at the layer (using forward hooks)
3. Sum over pixels of gradient maps to find the weights
4. Use the weights to weight and sum the activations maps of the convolutional layer
5. Pass through ReLU, resize to same image dimensions to obtain the Grad-CAM
6. \[Optional\] We can do backpropagation till the image to generate the image gradients. Then multiply with Grad-CAM to obtain Guided Grad-CAM

### Grad-CAM Answers "Why This Class ?"
![[Pasted image 20261019224009.png]]


![[Pasted image 20261019224100.png]]


# ViT: Is Attention an Explanation ?

![[Pasted image 20261019224218.png]]


# Explainability Scorecard

| Method                    | Answers "Why this class ?" | Needs from the model   | Costs                         |
| ------------------------- | -------------------------- | ---------------------- | ----------------------------- |
| Filters                   | no                         | weights                | free                          |
| Max-activating images     | no                         | a large photo set      | 1 forward pass per photo      |
| Occlusion / swap          | yes                        | nothing (black box)    | 1 forward pass per patch      |
| Gradients (Saliency)      | Yes, noisy                 | Gradients              | 1 backward pass               |
| CAM                       | yes                        | GAP + linear head      | free                          |
| Grad-CAM                  | yes                        | gradients at one layer | 1 backward pass; coarse (7x7) |
| Attention / rollout (ViT) | no: Class-agnostic         | Attention weights      | free                          |

> [!warning] What to start with
> - Start with **Grad-CAM**
> - Confirm with a **counterfactual** (Occlude or swap what it points at)


![[Pasted image 20261019224732.png]]




