---
title: Attention & Transformers
tags:
  - Attention
  - Transformers
---
# Why Attention ?
#RNN process sequences 1 token at a time.
This creates 2 problems:
1. They are slow to train because computation is sequential
2. Even LSTMs struggle with very long-range dependencies.

#Attention solves both problems by allowing each token to look directly at every other token.
Instead of passing information through hidden states step by step, attention computes:
> "How relevant is every token in the sequence to the current token"

Then it gathers information from all tokens in 1 step
This makes the model highly parallelizable and better at capturing long-range relationships.

## Self-Attention: Queries, Keys, Values

For every token embedding $x_i$ we create 3 vectors:
$q_{i} = W_{Q}x_{i}$
$k_{i} = W_{K}x_{i}$
$v_{i} = W_{V}x_{i}$

Where:
$W_{Q}$ , $W_{K}$ , $W_{V}$ are learned weight matrices
$q_{i}$ is the **query**: what this token is looking for
$k_{i}$ is the **key**: What this token contains
$v_{i}$ is the **value**: the actual content to pass if matched

The attention score between token $i$ and token $j$ is:
$score_{ij} = q_{i} \cdot k_{j}$
A high score means token $j$ is relevant to token $i$.

We then apply softmax over all $j$ producing attention weights:
$\alpha_{ij} = \frac{e^{score_{ij}}/{\sqrt{d_k}}}{\sum_{j}e^{score_{ij}}/\sqrt{d_k}}$

Finally, token $i$'s new representation is:
$output_{i} = \sum_{j} \alpha_{ij}v{j}$

This output is a weighted sum of all values
The weights come from query-key similarity

Because queries, keys and values all come from the same input sequence, this is called **self-attention**

### Worked Example
We have 3 token embeddings with $d = 2$
$x_1 = [1, 0], x_2 = [0, 1], x_3 = [1, 1]$

For simplicity, assume: $W_Q = W_K = W_V = I$

So: $q_i = k_i = v_i = x_i$

Compute the new representation for token 1:

1. Query-key score
$q_1 = [1, 0]$

$q_1 \cdot k_1 = 1$
$q_1 \cdot k_2 = 0$
$q_1 \cdot k_3 = 1$

Scores: $[1, 0, 1]$

2. Scale
$d_k = 2, \sqrt{d_k} = 1.414$
Scaled Scores: $[0.707, 0, 0.707]$

3. Softmax
$e^{0.707} = 2.028$
$e^{0} = 1$

Sum: $2.028 + 1 + 2.028 = 5.056$

Weights: 
$\alpha_{11} = 0.401$
$\alpha_{12} = 0.198$
$\alpha_{13} = 0.401$

4. Weighted sum of values
Values: $v_1 = [1, 0], v_2 = [0, 1], v_3 = [1, 1]$

Output for token 1:
$0.401[1,0] + 0.198[0, 1] + 0.401[1, 1]$
$= [0.401, 0] + [0, 0.198] + [0.401, 0.401]$
$= [0.802, 0.599]$

So token 1 now contains information from token 2 and token 3 as well.


## Scaled Dot-Product Attention

In matrix form, attention is computed as:
$Attention(Q,K,V) = softmax(\frac{QK^T}{\sqrt{d_k}})V$

Where:
$Q$ has shape (seq, $d_k$)
$K$ has shape (seq, $d_k$)
$V$ has shape (seq, $d_v$)

The division by $\sqrt{d_k}$ prevents dot products from becoming too large when $d_k$ is large.
Large dot products push softmax into regions with very small gradients, slowing learning.


## Multi-Head Attention
Instead of using 1 attention mechanism, we can use many.

Each head has its own $W_Q , W_K , W_V$
This allows different heads to learn different types of relationships:
- One head might learn syntactic dependencies
- Another might learn long-range semantic connections
- Another might focus on adjacent tokens

The outputs from all heads are concatenated and projected:
$MultiHead(Q, K, V) = Concat(head_1 , ... , head_h)W_O$

Where: $head_i = Attention(QW_{Qi} , KW_{Ki} , VW_{Vi})$

If $d_{model}$ = 512, we use $h = 8$ each head has dimension:
$d_k = \frac{512}{8} = 64$


## Transformer Block Overview

Consist of:
1. Multi-head self attention
2. Residual connection and layer normalization
3. Feed-forward network
4. Residual connection and layer normalization

In Pseudocode:
```python
def transformer_block(x):
	attn_out = multi_head_attention(x)
	x = layer_norm(x + attn_out)
	
	ff_out = feed_forward(x)
	x = layer_norm(x + ff_out)
	
	return x
```

Residual connections help gradients flow through deep networks
Layer normalization stabilizes training.









































