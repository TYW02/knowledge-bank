---
title: Sequence Models and RNN
tags:
  - RNN
  - Sequence_Model
  - LSTM
  - GRU
---
# Why Sequences are Different
Many Real-world data types have **order**:
- Text: "The cat sat on the mat"
- Time Series: Stock prices over days
- Audio: Speech Waveforms
- Video: Frames in time

In these cases, the order matters
"The cat sat" is different from "sat cat The".

A feedforward network treats each input independently and has no memory.
It cannot naturally capture:
- What came before ?
- What should come next ?
- How does the current input depend on the previous one ?

Recurrent Neural Networks #RNN solve this by adding a **hidden state** that carries information from previous time steps.

## RNN Hidden State

An RNN processes a sequence one element at a time.

At time step $t$, it takes:
- current input $x_t$
- previous hidden state $h_{t - 1}$
and produces:
- new hidden state $h_t$
- optional output $y_t$

The core equation is: $h_t = f(W_{h}h_{t-1} + W_{x}x_{t} + b)$

Where:
- $W_h$ is the weight matrix for the hidden state
- $W_x$ is the weight matrix for the input
- $b$ is the bias
- $f$ is an activation, often $tanh$

The output at time $t$ is: $y_t = g(W_{y}h_{t} + b{y})$
The same weights $W_{h}, W_{x}, W_{y}$ are reused at every time step.

This is the **key difference** from feedforward networks: The weights are shared across time.


### Numeric Example
Suppose: $h_{t} = tanh(0.5h_{t-1} + x_{t})$

Start with: $h_{-1} = 0$
Input Sequence: $x_1 = 1, x_2 = 0, x_3 = -1$

Step 1:
$h_1 = tanh(0.5 \cdot 0 + 1) = tanh(1) = 0.762$
Step 2:
$h_2 = tanh(0.5 \cdot 0.762 + 0) = tanh(0.381) = 0.364$
Step 3:
$h_3 = tanh(0.5 \cdot 0.364 -1) = tanh(-0.818) = -0.673$

Notice that $h_3$ depends on all previous inputs, not just $x_3$
The hidden state acts as memory.


## RNN Unrolled Through Time
$x_{1} -> RNN -> h_1 -> RNN -> h_2 -> RNN -> h_3$

The same RNN cell is copied at each time step.
The weights are shared

To train an RNN, we use backpropagation through time or BPTT

We unroll the network for a fixed number of steps, compute the loss over all outputs, and then propagate gradients backward through all time steps using the chain rule.


## Vanishing Gradients in Plain RNNs
A plain RNN has a serious problem with long sequences

During BPTT, gradient flows backward through time
At each step, it is multiplied by the recurrent weight matrix $W_h$
- If $W_h$ repeatedly multiplies values less than 1, the gradient shrinks exponentially.

For long sequences, this means:
- Early time steps receive almost no gradients
- The model cannot learn long-term dependencies

### Example
Sentence: "The cat, which was very hungry, finally sat on the mat"

To predict "sat", the model needs to remember "cat" from much earlier.
If the gradient vanishes, the model cannot learn that connection.

There is also an **exploding gradient** problem when weights are greater than 1 repeatedly, but gradient clipping can help.

## LSTM - Long Short-Term Memory
#LSTM

LSTM was designed to solve the vanishing gradient problem.

Instead of only a hidden state, an LSTM has 2 states:
1. Hidden State $h_t$ the output passed to the next step
2. Cell State $C_t$ a long-term memory highway.

The **Cell State** is modified by gates:
- Forget Gate: Decides what old information to remove
- Input Gate: Decides what new information to add
- Output Gate: Decides what to expose as the hidden state

The gates are vectors computed using #SigmoidFunction , so their values are between 0 and 1
0 means "close gate", 1 means "open gate"


### LSTM Equations
Given previous hidden state $h_{t-1}$ previous cell state $C_{t-1}$ and current input $x_t$

Forget gate: $f_t = \sigma(W_f[h_{t-1}, x_t] + b_f)$

Input Gate: $i_t = \sigma(W_i[h_{t-1}, x_t] + b_i)$

Candidate cell update: $C_t =  tanh(W_c[h_{t-1}, x_t] + b_C$

New cell State: $C_t = f_t \cdot C_{t-1} + i_t \cdot C_t$

Output Gate: $o_t = \sigma(W_o[h_{t-1}, x_t] + b_o)$

New Hidden State: $h_t = o_t \cdot tanh(C_t)$

### Intuition
The cell state $C_t$ acts like a conveyor belt
It flows through time with only small linear interactions.

The forget gate can keep old information if it outputs values near 1.
The input gate can add new important information
The output gate controls what part of the cell state becomes the hidden state

Because the cell state update is mostly additive
$C_t = f_t \cdot C_{t-1} + i_t \cdot C_t$
Gradients can flow through $C_t$ without being repeatedly squashed by activation functions.
This helps prevent vanishing gradients.


## GRU - Gated Recurrent Unit
#GRU

Simplified version of LSTM, combines cell state and hidden state into 1 hidden state

Use 2 gates:
- Reset Gate: Controls how much past information to forget
- Update Gate: Controls how much new information to add and how much past to keep

GRUs have fewer parameters than LSTMs and often perform similarly.

Many modern sequence models now use Transformers instead of RNNs, but LSTMs and GRUs are still useful for 
- Smaller datasets
- Time-Series forecasting
- Resource-Constrained Applications
- Sequence Tagging

## Character-Level Text Generation with LSTM
A classical way to understand RNNs is to train character-level text generator.

Task:
- Input: A sequence of characters
- Output: The next character in the sequence

The model learn patterns in text, like spelling, word boundaries, and even simple grammer.






























