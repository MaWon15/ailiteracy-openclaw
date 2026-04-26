# Chapter 19: Learning from Examples
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is Machine Learning?

**Machine learning:** A system improves its performance on a task through experience.

**Types of learning:**
- **Supervised learning:** Learn from labeled input-output pairs (x, y).
- **Unsupervised learning:** Find structure in unlabeled data.
- **Reinforcement learning:** Learn from rewards and penalties (see Chapter 22).
- **Semi-supervised learning:** Labeled + unlabeled data.
- **Self-supervised learning:** Labels derived from the data itself (e.g., predicting masked tokens).

## Supervised Learning Formalization

- **Training set:** {(x₁, y₁), ..., (xₙ, yₙ)} — pairs of input vectors and output labels.
- **Hypothesis h:** A function from inputs to outputs.
- **Goal:** Find h that generalizes well to unseen data.
- **Loss function L(y, h(x)):** Measures prediction error.
- **Empirical risk minimization (ERM):** Choose h minimizing average loss on training data.

## Decision Trees

- Tree structure: internal nodes = attribute tests, branches = attribute values, leaves = class labels.
- **Expressivity:** Can represent any Boolean function; arbitrary precision.

### Learning a Decision Tree (ID3/C4.5/CART)
**Splitting criterion:** Choose attribute that best separates examples by label.

**Information Gain (ID3):**  
Gain(A) = H(parent) − Σ_{v} |Sv|/|S| × H(Sv)

where H(S) = −Σₚ pₚ log₂(pₚ) is the **entropy** of set S.

**Gini impurity (CART):**  
Gini(S) = 1 − Σ pₖ²

**Overfitting prevention:**
- **Pruning:** Remove branches that don't improve validation accuracy.
- **Minimum examples per leaf.**
- **Early stopping.**

## Bias-Variance Tradeoff

- **Bias:** Error from incorrect assumptions (underfitting) — model is too simple.
- **Variance:** Error from sensitivity to training data (overfitting) — model too complex.
- **Bias-variance decomposition:** Expected loss = bias² + variance + noise.
- Complex models have low bias but high variance; simple models have high bias but low variance.

## Generalization and Overfitting

- **Training error** ≠ **test error**.
- **Overfitting:** Low training error, high test error — model memorizes training noise.
- **Underfitting:** High training and test error — model is too simple.
- **Model selection:** Choose complexity that minimizes generalization error (validation set, cross-validation).

**Occam's Razor:** Among hypotheses consistent with data, prefer the simplest.

## Linear Models

### Linear Regression
Predict a continuous output:  
h_w(x) = w⁰ + w₁x₁ + ... + wₙxₙ = w · x

**Loss:** Mean Squared Error (MSE) = (1/n) Σ (yᵢ − h_w(xᵢ))²

**Closed-form solution:** w = (XᵀX)⁻¹ Xᵀy (normal equations).

**Gradient descent:** wᵢ ← wᵢ − α ∂L/∂wᵢ.

### Logistic Regression (Classification)
Sigmoid function: h_w(x) = 1/(1 + e^(−w·x)) ∈ (0, 1).

Outputs a probability; threshold at 0.5 for binary classification.

**Loss:** Log loss / cross-entropy = −Σ [yᵢ log h(xᵢ) + (1−yᵢ) log(1−h(xᵢ))].

Optimized by gradient descent (no closed form).

## Support Vector Machines (SVMs)

Find the **maximum-margin hyperplane** separating two classes.

- **Support vectors:** Training points closest to the decision boundary.
- **Margin:** Distance between support vectors and the hyperplane.
- **Hard-margin SVM:** Assumes linearly separable data.
- **Soft-margin SVM:** Allows misclassifications with penalty C.

**Kernel trick:** Map features to higher-dimensional space implicitly.  
K(xᵢ, xⱼ) replaces xᵢ · xⱼ; allows nonlinear boundaries.
- **Polynomial kernel:** K(x, x′) = (x·x′ + 1)^d.
- **RBF (Gaussian) kernel:** K(x, x′) = exp(−‖x−x′‖²/(2σ²)).

SVMs have strong theoretical guarantees (VC dimension, PAC learning).

## Ensemble Methods

### Bagging (Bootstrap Aggregating)
- Train multiple classifiers on different random subsets (with replacement) of training data.
- Aggregate predictions (majority vote or average).
- **Reduces variance.**
- **Random Forests:** Bagging of decision trees with random feature subsets.

### Boosting
- Train classifiers sequentially; each focuses on the mistakes of the previous.
- **AdaBoost:** Weight misclassified examples more; combine weak classifiers into strong one.
- **Gradient Boosting / XGBoost:** Additive model where each new tree corrects residuals.
- **Reduces bias and variance;** very powerful in practice.

## Nonparametric Methods

### k-Nearest Neighbors (k-NN)
- Classify x by majority vote of the k nearest training points.
- **Non-parametric:** No explicit training; all computation at test time.
- **Lazy learning.**
- Sensitive to irrelevant features and scale.

### Kernel Regression
- Weighted average of nearby training outputs.
- Weights given by kernel function K(xᵢ, x).

## Model Evaluation

- **Hold-out validation:** Split data into train/validation/test.
- **k-fold cross-validation:** Partition data into k folds; train on k−1, validate on 1, rotate.
- **Leave-one-out (LOO):** Extreme case of k-fold (k = n).

**Evaluation metrics:**
- **Accuracy:** Fraction correct (misleading with class imbalance).
- **Precision / Recall / F1:** For imbalanced classification.
- **AUC-ROC:** Area under receiver operating characteristic curve.
- **RMSE:** Root mean squared error for regression.

## Key Terms

- **Supervised learning:** Learn from labeled examples.
- **Decision tree:** Tree classifier; nodes = attribute tests; leaves = labels.
- **Overfitting:** Model performs well on training data but poorly on test data.
- **Bias-variance tradeoff:** Tension between model simplicity (bias) and complexity (variance).
- **SVM:** Maximum-margin linear classifier; kernel trick allows nonlinear boundaries.
- **Ensemble method:** Combine multiple models to reduce error (bagging, boosting).
- **Cross-validation:** Technique to estimate generalization error.
- **Information gain:** Entropy-based criterion for choosing splits in decision trees.
