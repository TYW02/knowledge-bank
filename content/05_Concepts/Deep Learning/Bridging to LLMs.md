---
title: Bridging to LLMs
tags:
  - LLM
  - Tokenization
  - Embedding
---
LLMs like GPT are essentially stacks of transformer blocks trained on huge amounts of text.

# Tokenization & Embedding

Computers cannot process raw text directly, they need numbers.

But text is not naturally split into fixed-size numeric vectors like images.
So we break text into small units called **tokens**

A token can be:
- Word
- Subword
- Character
- Punctuation mark
Most modern LLMs use **subword tokenization**, often Byte-Pair Encoding or similar

Subword tokenization breaks rare or unknown words into smaller pieces while keeping frequent words whole.

### Example:
The word "unhappiness" might be tokenized as:
- "un"
- "happiness"

or "Playing" as:
- "Play"
- "ing"
 This allows the model to handle new words by combining known subwords.
After tokenization, each token is assigned an **integer ID** from a fixed vocabulary.

### Example simplified vocabulary:
| Token   | ID  |
| ------- | --- |
| "hello" | 0   |
| "world" | 1   |
| ","     | 2   |
| "!"     | 3   |
| "the"   | 4   |
| "cat"   | 5   |
| "sat"   | 6   |
| "on"    | 7   |
| "mat"   | 8   |
| "."     | 9   |
Sentence: "hello world, the cat sat on the mat."
Tokenized: ["hello", "world", ",", "the", "cat" , "sat" , "on" , "the" , "mat" , "."]
IDs: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

These IDs are the raw input to the model

# Embeddings
An integer ID is just an index
It does not contain any meaning.

So we map each token ID to a dense vector called an **embedding**
For a vocabulary of size $V$ and embedding dimension $d$, we create an embedding matrix $E$ of shape $V$ x $d$

The embedding for token ID $i$ is simply row $i$ of $E$
These embeddings are learned during training.
Tokens with similar meanings end up with similar vectors

So: [0, 1, 2, ...] -> Embedding layer -> matrix of shape (seq_len, d)

After embedding, we often add **positional encoding** so the model knows the order of tokens, because self-attention itself is permutation-invariant

## Pre-training VS Fine-Tuning

### Pre-training
Modern LLMs are first pre-trained on a massive amount of unlabeled text.
The pre-training task is almost always next-token prediction

Given a sequence of tokens: $x_1, x_2, ... , x_t$
The model predicts $x_{t+1}$

For example: 
Input: "The cat sat on the"
Target: "cat sat on the mat"

The model outputs a probability distribution over the vocabulary for each position.
We train it with cross-entropy loss, comparing predicted distribution to the actual next token.

This is **self-supervised** because the labels come from the text itself
No human labelling is needed.

During pre-training, a **causal mask** is used in self-attention.
Each token can only attend to itself and previous tokens, not future tokens.
This is essential for next-token prediction, otherwise the model would cheat.

This is also why GPT is called decorder-only and autoregressive.

## Fine-tuning
Pre-training gives the model broad language understanding, but it is not yet specialized for instructions or tasks.

Fine-tuning adapts the pre-trained model to a specific task or style.

There are several fine-tuning approaches:
1. **Supervised fine-tuning** on instruction-response pairs
2. **Reinforcement learning from human feedback** of RLHF to align with human preferences
3. **Prompt tuning** or **LoRA** for parameter-efficient adaptation.
During fine-tuning, the model is usually trained on a much smaller, curated dataset.
The weights from pre-training are used as a starting point.

## Sampling: Temperature, Top-k, Top-p
After training, the model outputs **logits** for the next token

We need to choose which token to generate.
The simplest method is greedy decoding: Always pick the token with the highest probability.
But greedy decoding is deterministic and often repetitive

We can instead sample from distribution.
This introduces randomness, but we need to control it

## Temperature
Temperature scales the logits before softmax

Let $z_i$ be the logits:
Instead of: $P_i = \frac{e6{z_i}}{\sum_{j}e^{z_{j}/T}}$
Where $T$ is the temperature
- $T < 1$: logits become more extreme -> distribution becomes sharper -> less random, more confident
- $T > 1$: logits become more uniform -> distribution becomes flatter -> more random, more diverse
- $T = 1$: standard softmax

### Example
Logits: $z = [2.0, 1.0, 0.1]$

With $T = 0.5$: 
$z/T = [4.0, 2.0, 0.2]$

Softmax: $[0.844, 0.114, 0.042]$

The model heavily favors the first token.
With $T = 2.0$:
$z/T = [1.0, 0.5, 0.05]$

Softmax: $[0.422, 0.256, 0.322]$
This distribution is much flatter.

## Top-k Sampling
Top-k sampling restricts sampling to the $k$ most likely tokens
1. Take the top $k$ logits
2. Recompute softmax over only those $k$ tokens
3. Sample from that new distribution

This prevents the model from choosing very unlikely tokens.

Example: $k = 3$ for a vocabulary of 10 tokens
Only the 3 most likely tokens are considered.
If $k$ is small, the model becomes more conservative
If $k$ is large, more diversity

## Top-p Sampling (Nucleus Sampling)
Top-p sampling chooses the smallest set of tokens whose cumulative probability is at least $p$.

1. Sort probabilities descending
2. Add tokens until the cumulative sum reaches $p$
3. Recompute softmax over that set
4. Sample from that set

This dynamically adapts the number of candidate tokens.

Example: $p = 0.9$ means we keep the tokens that together account for 90% of the probability mass.

If the model is very confident, few tokens are kept.
If unsure, many tokens are kept.

# GPT-Style Models Overview
GPT stands for Generative Pre-trained Transformer

It is a stack of transformer **decoder** blocks

Key properties:
- Autoregressive: Generate 1 token at a time, left to right
- Causal masking: Each token attends only to previous tokens
- Pre-trained with next-token prediction on huge text corpora
- Self-supervised: No human labels needed for pre-training

Training Pipeline:
1. Pre-train on raw text
2. Fine-tune on task-specific data or instruction tuning
3. Optionally align with RLHF

Scaling laws show that increasing model size, data, and compute improves performance predictably.
Modern LLMs are often called **decoder-only** because they do not use the full encoder-decoder transformer structure.
They use only the decoder part with causal self-attention






















































