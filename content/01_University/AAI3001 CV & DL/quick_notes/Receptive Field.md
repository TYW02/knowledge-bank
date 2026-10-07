
# What it is

> [!important] Main Idea: Receptive Field
> Region of the **input** (original image) that can influence that neuron's output. As you go **deeper** into a CNN, each neuron "**sees**" a **larger region** of the **input** because it **aggregates information from previous layers**

- RF grows with **depth**, **larger kernels**, **larger strides**, and **dilation**

## Single vs Stacked Convolution
| Feature         | Single 5 x 5      | Stacked 3 x 3     |
| --------------- | ----------------- | ----------------- |
| Parameters      | Higher            | Lower             |
| Non-Linearity   | Single Activation | Double Activation |
| Receptive Field | Both are 5 x 5    | Both are 5 x 5    |

## Effective Receptive Field
> The total size of the region in the original input that influences a specific feature in a higher layer.


# Key Quantities to Track

| Quantity | Meaning                                                                                   |
| -------- | ----------------------------------------------------------------------------------------- |
| `RF`     | Receptive field size of the current layer (in input pixels)                               |
| `jump`   | Distance between two adjacent features in the current layer, measured in **input pixels** |
| `start`  | Center coordinate of the first feature in the current layer, in input pixels              |

## The update formula
For a layer with kernel size `k`, stride `s` and dilation `d`:
### Effective kernel size:
$$
k_{eff} = (k - 1) \cdot d + 1
$$
### New receptive field
$$
RF_{out} = RF_{in} + (K_{eff} - 1) \cdot jump_{in}
$$
### New Jump
$$
jump_{out} = jump_{in} \cdot s
$$
- **Padding doesn't change** the **receptive field size** but shifts where the center sits
- For **pooling layers**, use the **same formulas** with the pooling kernel size and stride

## Worked examples

### Example 1: Three stacked 3×3 convs, stride 1

|Layer|k|s|RF|jump|start|
|---|---|---|---|---|---|
|Input|—|—|1|1|0.5|
|Conv1|3|1|1 + 2·1 = **3**|1|0.5 + 1·1 = 1.5|
|Conv2|3|1|3 + 2·1 = **5**|1|1.5 + 1·1 = 2.5|
|Conv3|3|1|5 + 2·1 = **7**|1|2.5 + 1·1 = 3.5|

Three 3×3 convs have the same RF as one 7×7 conv, but with fewer parameters (3 × 9 = 27 vs 49) and more nonlinearity. This is why VGG stacks small kernels.

### Example 2: Conv 3×3, then 2×2 maxpool stride 2, then conv 3×3

|Layer|k|s|RF|jump|start|
|---|---|---|---|---|---|
|Input|—|—|1|1|0.5|
|Conv1|3|1|1 + 2·1 = **3**|1|1.5|
|Pool1|2|2|3 + 1·1 = **4**|2|1.5 + 0.5·1 = 2.0|
|Conv2|3|1|4 + 2·2 = **8**|2|2.0 + 1·2 = 4.0|

The final conv has RF = 8 in the input.

> [!important] About Stride
> A layer's **OWN** stride **does NOT affect its own** RF contribution


# My Example

Say you have:
- Conv1: Kernel `3x3`, Stride = `1`
- Conv2: Kernel `3x3`, Stride = `1`
- Pool1: Kernel `2x2`, Stride = `2`
- Conv3: Kernel `3x3`, Stride = `1`
- Conv4: Kernel `3x3`, Stride = `2`
- Pool2: Kernel `2x2`, Stride = `2`
- Conv5: Kernel `3x3`, Stride = `1`

Formula:
$$
RF = RF_{current} + (Kernel - 1) \cdot (Product\_of\_all\_previous\_stride)
$$

So:
- Conv1: 1 + 2 * 1 = 3
- Conv2: 3 + 2 * 1 = 5
- Pool1: 5 + 1 * 1 = 6
- Conv3: 6 + 2 * 2 = 10
- Conv4: 10 + 2 * 2 = 14
- Pool2: 14 + 1 * 4 = 18
- Conv5: 18 + 2 * 8 = **34**

Final RF = **34**


## With Dilation

Formula:
$$
RF = RF_{current} + (Kernel - 1) \cdot (dilation) \cdot (Product\_of\_all\_previous\_stride)
$$


### Example: 

- Conv1: Kernel: `3x3`, Stride = 2
- Conv2: Kernel: `3x3`, d=2, Stride=1

Calculation:
- Conv1: 1 + (2) * 1 = 3
- Conv2: 3 + (2) * 2 * 2 = **11**

Final RF: **11**



### Example: 

- Conv1: Kernel: `3x3`, d = 1
- Conv2: Kernel: `3x3`, d=2
- Conv2: Kernel: `3x3`, d=4

Calculation:
- Conv1: 1 + (2) * 1 = 3
- Conv2: 3 + (2) * 2 * 1 = 7
- Conv2: 7 + (2) * 4 * 1 = **15** 

Final RF: **15**









