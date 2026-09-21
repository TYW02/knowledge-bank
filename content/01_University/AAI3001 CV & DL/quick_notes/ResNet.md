
# Characteristics
- Regular stack of many residual blocks
- HEAVY use of Batch normalization
- Regular design akin to VGG
- Multiple regular stages
	- First reduce the resolution by half using stride 2 conv
	- Double the number of channels
- Adapted aggressive resolution reduction and global average pooling from GoogLeNet (Inception Block)


## Why do residual connections work ?
- Gradient Perspective: Gradient flows as the **identity** through the shortcut, **NO vanishing** gradient problem
- Shortcut in **forward pass** inputs feature x from previous block convolutions across the residual path can learn **additionally non-linear** function on top
- If identity mapping **f(x)=x** is desired, the residual mapping **g(x)=0 goes to zero**, which is **easier** to learn
- Option for quick **unlearning** to identity: If **poor fit** was learned during early phases of training, it can be **undone**: Update **weights of convolution** layers to **zero**, then get back the **identity** again.



























































