# Chapter 20: Learning Probabilistic Models
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Learning and Probability

Supervised learning with probabilistic outputs is a natural extension:  
Instead of predicting a class label, predict a **probability distribution** over outcomes.

Probabilistic models are learned from data via **maximum likelihood estimation (MLE)** or **Bayesian parameter estimation**.

## Statistical Learning

### Maximum Likelihood Estimation (MLE)
Given data **d** = {x₁, ..., xₙ}, find parameters θ that maximize P(d | θ):  
θ_MLE = argmax_θ P(d | θ) = argmax_θ Σᵢ log P(xᵢ | θ)

- For a coin: θ_MLE = heads/total — the frequency estimate.
- **Asymptotically consistent:** θ_MLE → true θ as n → ∞.
- **Overfits with small data** — e.g., 1/1 heads gives P(heads) = 1.

### Bayesian Parameter Estimation
Treat θ as a random variable:  
P(θ | d) = P(d | θ) × P(θ) / P(d)  (Bayes' Rule)

- **Prior P(θ):** Encodes beliefs before seeing data.
- **Posterior P(θ | d):** Updated belief.
- **Prediction:** P(x | d) = ∫ P(x | θ) P(θ | d) dθ (marginalizes over uncertainty in θ).

For discrete events, using a **Dirichlet prior** is conjugate to a multinomial likelihood — posterior is also Dirichlet.

**Laplace smoothing (add-one smoothing):** Add 1 to each count before normalizing — equivalent to a uniform Dirichlet prior. Avoids zero-probability issues.

## Learning Bayesian Network Parameters

Given a fixed network structure and complete data:
- Each CPT can be estimated independently.
- MLE: θ_{xᵢ | parents} = count(Xᵢ = xᵢ, Parents = parents) / count(Parents = parents).
- Bayesian: Use Dirichlet priors for each CPT entry.

### Missing Data and the EM Algorithm

When some variables are **unobserved (latent)**:
- Direct MLE is intractable (gradient landscape has many local maxima).
- **Expectation-Maximization (EM) algorithm** iterates:
  1. **E-step:** Compute expected values of hidden variables given current parameters (soft assignments).
  2. **M-step:** Update parameters to maximize the expected log-likelihood.
- **Converges** to a local maximum of the likelihood (not necessarily global).

## Learning Bayesian Network Structure

**Structure learning:** Find the network topology that best explains the data.

### Score-Based Methods
- **BIC (Bayesian Information Criterion):** BIC = log P(d | θ_MLE) − (k/2) log n
  - Penalizes complexity (k = number of parameters).
  - Asymptotically selects the correct structure.
- **BDe score (Bayesian Dirichlet equivalent):** Bayesian score with Dirichlet priors.
- **Search:** Greedy hill-climbing, genetic algorithms, beam search over DAG space.

### Constraint-Based Methods
- Use conditional independence tests (χ² test, mutual information) to discover the skeleton and orientation.
- **PC algorithm:** Starts with a complete graph, removes edges that pass CI tests, then orients edges.
- **IC algorithm (Inductive Causation):** Similar; can identify causal structure under faithfulness assumption.

## Density Estimation

Learn a probability distribution over the feature space.

### Gaussian Mixture Models (GMMs)
- Mixture of K Gaussian components:  
  P(x) = Σₖ πₖ N(x | μₖ, Σₖ)
- πₖ = mixing weights, Σπₖ = 1.
- **Fitted via EM:**
  - E-step: Compute posterior probabilities (responsibilities) of each component for each data point.
  - M-step: Update πₖ, μₖ, Σₖ from weighted data.
- **K-means** is a special case (hard assignments, spherical Gaussians, fixed variance).

### Naive Bayes Revisited
- Generative model: P(class, features) = P(class) Π P(featureᵢ | class).
- Parameters estimated by MLE (or MAP).
- Discriminative analogs (logistic regression) often perform better when features are correlated.

## Generative vs. Discriminative Models

| | Generative | Discriminative |
|---|---|---|
| Models | P(X, Y) | P(Y | X) |
| Examples | Naive Bayes, HMM, GMM | Logistic regression, SVM, CRF |
| Training data | Can use unlabeled data | Requires labels |
| Performance | Often worse with much labeled data | Often better with much labeled data |

**Conditional Random Fields (CRFs):**
- Discriminative model for sequence labeling (e.g., NER, POS tagging).
- Models P(Y | X) where Y is a sequence of labels.
- Features can include arbitrary context (unlike HMMs).

## Nonparametric Density Estimation

### Kernel Density Estimation (KDE)
P(x) = (1/n) Σᵢ K_h(x − xᵢ)  

where K_h is a kernel (e.g., Gaussian) with bandwidth h.

- **Too small h:** Spiky, overfit.
- **Too large h:** Over-smoothed, underfit.
- Bandwidth selection via cross-validation.

## Latent Variable Models

**Latent variables:** Unobserved random variables that explain correlations in data.

- **PCA (Principal Component Analysis):** Linear latent variable model; finds directions of maximum variance.
- **Factor Analysis:** Gaussian latent variables with linear factor loadings.
- **Topic Models (LDA):** Latent Dirichlet Allocation — each document is a mixture of topics; each topic is a distribution over words.
  - Inference via EM or variational Bayes.
  - Widely used for text analysis.

## Key Terms

- **MLE:** Maximum Likelihood Estimation — find parameters maximizing data probability.
- **Bayesian estimation:** Treat parameters as random variables; maintain posterior distribution.
- **Laplace smoothing:** Add small counts to avoid zero probabilities; equivalent to uniform prior.
- **EM algorithm:** Iterative procedure for MLE/MAP with latent variables.
- **GMM:** Gaussian Mixture Model — soft-clustering density estimator fitted by EM.
- **Generative model:** Models joint distribution P(X, Y).
- **Discriminative model:** Models conditional P(Y | X) directly.
- **Structure learning:** Learn the topology of a Bayesian network from data.
- **LDA:** Topic model using latent Dirichlet-distributed topics.
