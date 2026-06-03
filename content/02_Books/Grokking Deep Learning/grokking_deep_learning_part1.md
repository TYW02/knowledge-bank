# Grokking Deep Learning — Part 1: Neural Network Basics
## Knowledge Base Entry

---

## Overview

Part 1 builds the foundational mental operating system for all of deep learning. Every concept that follows — transformers, attention, LLMs — is an elaboration of what is established here. The central question Part 1 answers is:

> **How does a machine change its own behavior based on evidence?**

---

## Core Concepts

### 1. The Prediction-Error-Correction Loop

The heartbeat of all deep learning. Learning is never about finding the right answer directly. It is about **reducing a mistake, repeatedly**.

The loop:
1. Make a prediction using current weights
2. Measure how wrong the prediction was (calculate error)
3. Use that error to correct the weights
4. Repeat

**Key insight:** A network with random weights can learn because it has a mechanism to measure its own mistakes and correct them iteratively.

---

### 2. Weights — The Memory of the Network

Weights are not just numbers. They are the **accumulated memory of every correction the network has ever made**. Every weight update encodes what the network has learned from its mistakes.

**Prediction equation:**
```
prediction = input × weight
```

---

### 3. Error Calculation — Why We Square It

```
error = (prediction - target)²
```

We square the error for two reasons:

- **Prevent cancellation:** Positive and negative errors would cancel out if summed directly, masking how wrong the model truly is
- **Amplify larger errors:** Squaring scales up bigger mistakes, forcing the model to prioritize reducing large errors

**Key distinction:** `prediction` is what the model outputs. `target` is the correct answer. Their difference is how wrong the model was.

---

### 4. The Derivative — A Compass for Learning

The derivative of the error with respect to a weight tells us the **slope of the error surface** at the current weight value. It answers:

> If I nudge this weight slightly, does the error go up or down?

**Critical rule:** We move the weight in the **opposite direction** of the derivative.

- Positive slope → decrease the weight
- Negative slope → increase the weight

Moving in the same direction as the slope would increase error and move further from the solution.

---

### 5. Deriving the Weight Update — First Principles

Starting from the error function:
```
error = ((input × weight) - target)²
```

Let `u = (input × weight) - target`, so `error = u²`

Applying the chain rule:

**Step 1 — Differentiate the outside:**
```
d(error)/du = 2u
```

**Step 2 — Differentiate the inside with respect to weight:**
```
d(u)/d(weight) = input      (target is a constant → drops to zero)
```

**Combining both steps:**
```
full derivative = 2 × ((input × weight) - target) × input
               = 2 × error × input
```

The `2` is absorbed into the learning rate in practice, leaving:
```
weight_update = error × input
new_weight = old_weight - (learning_rate × error × input)
```

---

### 6. Why Input Appears in the Weight Update — The Principle of Proportional Credit

> A weight is only responsible for the error it actually caused.

If `input = 0`:
```
weight_update = error × 0 = 0
```

The weight does not update at all — because it contributed nothing to the prediction, it deserves no blame for the mistake. This is not just mathematical convenience. It is a **fairness mechanism** baked into the mathematics of learning.

**Practical implication:** Weight updates are always proportional to how much that weight participated in producing the wrong answer.

---

### 7. The Learning Rate — Controlling Step Size

```
new_weight = old_weight - (learning_rate × weight_update)
```

The learning rate prevents **overshooting** — taking steps so large that the weight flies past the optimal value and makes things worse.

| Learning Rate | Problem |
|---|---|
| Too high | Overshoots, weights become unstable, error increases |
| Too low | Learning is extremely slow, may never converge |
| Just right | Steady, stable convergence toward minimum error |

**Analogy:** The derivative tells you which direction to walk. The learning rate tells you how big each step to take.

---

### 8. Feature Scaling — A Critical Practical Requirement

**The problem:** When input features exist on vastly different scales, weight updates become unbalanced.

Example with the same error value of 5:
```
input = 0.01  →  weight_update = 5 × 0.01 = 0.05
input = 100   →  weight_update = 5 × 100  = 500
```

The weight connected to the larger input dominates training entirely. The smaller input's weight barely moves.

**The solution — apply before training:**

Normalisation (scale to 0-1 range):
```
scaled = (value - min) / (max - min)
```

Standardisation (scale to mean=0, std=1):
```
scaled = (value - mean) / standard_deviation
```

**Common junior engineer mistake:** Feeding raw unscaled data into a model, watching it train poorly, and blaming the architecture. The problem is almost always the data.

---

### 9. The Compounding Problem in Deep Networks

In a single neuron, unscaled inputs cause one weight to dominate. In a deep network, the output of one layer becomes the **input to the next layer**. The imbalance compounds through layers:

```
Layer 1: unscaled inputs → unbalanced outputs
Layer 2: receives unbalanced outputs as inputs → worse imbalance
Layer 3: receives even more distorted values
...
```

This leads to two major failure modes:

- **Vanishing gradients:** Updates become so tiny that weights in early layers stop learning entirely
- **Exploding gradients:** Updates become so large that weights become numerically unstable

Both trace directly back to scaling problems at the input level.

---

## Key Formulas Reference

| Formula | Purpose |
|---|---|
| `prediction = input × weight` | Forward pass — making a prediction |
| `error = (prediction - target)²` | Measuring how wrong the prediction was |
| `weight_update = error × input` | How much and in what direction to correct |
| `new_weight = old_weight - (lr × weight_update)` | Applying the correction |

---

## Calculus Rules Used in Backpropagation

| Rule | Formula | Example |
|---|---|---|
| Constants vanish | `d(constant)/dx = 0` | `d(target)/d(weight) = 0` |
| Power rule | `d(xⁿ)/dx = n × x^(n-1)` | `d(x²)/dx = 2x` |
| Chain rule | `d(f(g(x)))/dx = f'(g(x)) × g'(x)` | Applied to `(u)²` where `u = input×weight - target` |

---

## Mental Models to Retain

**The blind hiker:** Gradient descent is a blind hiker on a foggy hill, finding the lowest valley by feeling only the slope beneath their feet. The derivative is the slope. The learning rate is the step size.

**Fairness of blame:** Weights are only penalised in proportion to their contribution to the mistake. Zero input = zero blame = zero update.

**Weights as memory:** Every weight update is the network remembering a correction. Weights encode the history of every mistake the network has been penalised for.

---

## Connections to Future Concepts

| Part 1 Concept | Where It Appears Later |
|---|---|
| Weights and matrix multiplication | Foundation of every transformer layer |
| Gradient descent | Trains GPT, Claude, and every modern LLM |
| Loss functions | Used in RLHF to align language models to human preferences |
| Prediction-correction loop | Identical structure to ChatGPT fine-tuning on human feedback |
| Vanishing/exploding gradients | Core motivation for residual connections, batch normalisation, careful weight initialisation |
| Feature scaling | Required preprocessing step in all production ML pipelines |

---

## Interview Questions This Chapter Prepares You For

- Why do we square the error instead of taking the absolute value?
- What happens to a weight update when the input is zero, and why does that make sense?
- What is the learning rate and what happens when it is too high or too low?
- Why must features be scaled before training a neural network?
- What are vanishing and exploding gradients and what causes them?
- Explain gradient descent from first principles without using jargon.

---

## Knowledge Gaps Identified in Review

- Calculus differentiation mechanics were not previously understood — now addressed through the power rule and chain rule
- The intuition for *why* input appears in the weight update needed to be built from the zero-input edge case rather than stated directly

---

*Reviewed via Socratic session. Mastery verified at levels 1–4. Chapter considered complete.*
