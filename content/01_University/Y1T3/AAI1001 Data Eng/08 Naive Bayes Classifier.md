---
title: 08 Naive Bayes Classifier
tags:
  - Bayes
---
# Setting the Scene
Every day, thousands of customer browse your website, but only ~40% make a purchase
You want to predict which customers are about to buy

The underlying question is: Which "Signals" actually predict a purchase ?
The "magic" is in how you reach a meaningful probability, interpreted as which features to use, and how to combine them into a prediction. This is where Naive #Bayes comes in.

# 1st Feature is_member (Bernoulli Feature)
Is the customer a registered member ?
Hypothesis: Members are more likely to buy than non-members.
y = Purchase Outcome, x = is_member

Bayes Formula: $P(y|x) = \frac{P(x|y)P(y)}{P(x)}$

![[Pasted image 20260710170910.png]]This is for every combination of X and y: Yes member & Didn't buy, Yes member & Buy, No Member & Didn't buy, No Member & Buy

Predict $\hat{y} = argmax(P(y|x))$

## List of Terms

### Posterior
$P(y|x)$: Probability of each class label given the observed feature. This is what we want to solve

### Likelihood
$P(x|y)$: Meaning given to observed class label $y$, how likely does it correspond to the feature $x$

### Prior
$P(y)$: Marginal probability of each purchase outcome before observing any feature, estimated directly from training data

### Evidence
$P(x)$: Marginal distribution of `feature` across all regardless of outcome. Can be canceled out when comparing $P(y|x)$ across classes.

![[Pasted image 20260710171744.png]]
We take the argmax so for example: Since x = Y and y = Y is bigger than x = N and y = N we take 0.549.
Which means that if the customer is a member we can predict as they purchased something.

![[Pasted image 20260710172021.png]]
```R
ml <- e1071::naiveBayes(purchased ~ is_member, data = train, laplace = 0)

pred_train <- predict(ml, train)
pred_test <- predict(ml, test)
cat("Training Accuracy:", round(mean(pred_train == train$purchased), 3), "\n")
cat("Test Accuracy:", round(mean(pred_test == train$purchased), 3), "\n")
```

The first line of code means that we are trying to predict `purchased` from the `is_member` column, and laplace is used to avoid zero probability.

#### Threshold Tuning
The default is P > 0.5 but we can raise P > 0.7 to cut costly FP, or lower to catch more buyers at the cost of more FP.
The right threshold depends on the business cost of each error type.

#### Uncertainty Awareness
A posterior near 0.5 signals that the model genuinely does not know (Kind of like accuracy = 0.5 is no better than guessing).
Here collect more features for that customer before deciding.

# 2nd Feature product_category (Categorical Feature)
Which product type is the customer browsing ?
Hypothesis: Product category reveals purchase intent. Example: Food is impulse buy, while electronics requires research and comparison, so fewer browsers complete the purchase.

> [!NOTE]
> We now denote `is_member` as $x_1$ and `product_category` as $x_2$. Purchase outcome is still $y$

$x_2$ takes $k = 4$ unordered values: $x_2^{(1)} Electronics, x_2^{(2)} Beauty, x_2^{(3)} Clothing, x_2^{(4)} Food$

![[Pasted image 20260710172939.png]]
$P(y) and P(x_1|y)$ are already known from feature 1. The new term to estimate is $P(x_2^{(i)})| y)$

### Categorical Likelihood for $x_2^{i}$
$P(x_2^{(i)}|y) = (count(x_2^{(i)}, y) / (count(y))$

Updated Decision Rule: Predict = $\hat{y} = argmax P(y)P(x_1|y)P(x_2^{(i)}|y))$
![[Pasted image 20260710173414.png]]


# 3rd feature: purchase_history (Multinomial Feature)
How many previous purchase the customer has made ?
Hypothesis: Each past purchase is evidence of platform trust. More past purchase means stronger buying intent signal

![[Pasted image 20260710173703.png]]

## Intuition behind $C$ and $P(x_3|y)$

If count = 0 meaning no previous purchase
Then $P(x_3|y)^0 = 1$ which contributes no information for this feature.

Since buyers tend of have more total past purchases using:
$P(x_3|y = Y)^C / P(x_3|y = N)^C$ amplifies the Yes advantage


# 4th Feature session_duration_min (Gaussian Feature)
How long the customer spent browsing the platform ?
Hypothesis: Engaged shoppers spend more time viewing and comparing products, signaling stronger purchase intent.

![[Pasted image 20260710174341.png]]

## Intuition behind $\hat{\mu_y}$ and $\hat{\sigma_y}$

$\hat{\mu}_{y} = Y > \hat{\mu}_{y} =  N$: Buyers spend more time on average
$\hat{\sigma}_{y} = Y$ and $\hat{\sigma}_{y} =  N$: Quantify how spread the durations are

As $x_4$ increases beyond $\hat{\mu}_y = N$ the ratio $P(x_4|y = Y) / P(x_4|y = N)$ grows: Longer sessions amplify the Yes advantage.
![[Pasted image 20260710174922.png]]


# Putting it All Together
![[Pasted image 20260710175032.png]]

- Test accuracy increases from Model 1 to Model 4 as each new feature is added.
- Train accuracy does not always follow
- **IMPORTANT**: Adding more features is not always better
- Model 5 uses only 3 features yet scores lower than the 4 feature Model 4
- Feature selection matters more than feature count alone.


# When Naive Bayes Gets It Wrong
Naive Bayes assumes features are **Independent**
- But a frequent buyer is very likely to be a member too!
![[Pasted image 20260710175730.png]]

$x_1$ and $x_3$ carry overlapping information leading to **double-counts**
- Consequences could be overconfident predictions
![[Pasted image 20260710175737.png]]
## Naive Bayes Strengths
- Fast training and prediction, scales to millions of features
- Works well even with small training datasets
- Handles missing features gracefully at prediction time (If missing, it is excluded **ONLY** when calculating frequencies or probabilities)
- Naturally probabilistic: Outputs a full posterior distribution
- No complex hyperparameter tuning (Only Laplace smoothing)
- Strong baseline for text and high-dimensional data

## Naive Bayes Limitation
- Conditional independence assumption is rarely exactly true
- Probabilistic are poorly calibrated: Tends to be overconfident
- Cannot capture interactions between features
- Gaussian assumption may fail for skewed or multimodal features
- Correlated features double-count evidence and inflate confidence
- May underperform tree-based or gradient boosting models on large structured data


# Formal Notation
![[Pasted image 20260710175717.png]]



















