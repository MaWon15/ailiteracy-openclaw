# Chapter 13: Probabilistic Reasoning
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Bayesian Networks

A **Bayesian network (BN)** (also: belief network, probabilistic graphical model) is a compact representation of a joint probability distribution.

### Structure
- **Directed acyclic graph (DAG):** Nodes = random variables; edges = direct probabilistic influences.
- **Conditional Probability Table (CPT):** For each node Xᵢ, stores P(Xᵢ | Parents(Xᵢ)).
- No CPT needed for roots (nodes with no parents) — just their marginal prior.

### Semantics
The joint distribution is:  
P(X₁, ..., Xₙ) = ∏ᵢ P(Xᵢ | Parents(Xᵢ))

This factored representation requires far fewer parameters than the full joint distribution.

### Example: Alarm Network
Variables: Burglary (B), Earthquake (E), Alarm (A), JohnCalls (J), MaryCalls (M).
- B and E are root nodes.
- A depends on B and E: CPT has 4 entries.
- J and M each depend only on A.
- Total parameters: 1 + 1 + 4 + 2 + 2 = 10 (vs. 31 for full joint with 5 binary variables).

### Constructing Bayesian Networks
1. Identify relevant variables.
2. Order variables (causes before effects is natural).
3. Add edges reflecting direct influences.
4. Fill in CPTs from data or expert knowledge.

**Markov blanket:** A node's parents, children, and children's other parents. A node is conditionally independent of all other nodes given its Markov blanket.

## Conditional Independence and d-Separation

**d-separation:** A graphical criterion for reading conditional independencies from a BN structure.

### Three Connection Types (along a path):
1. **Causal chain:** X → Z → Y — X ⊥ Y | Z (Z blocks the path).
2. **Common cause:** X ← Z → Y — X ⊥ Y | Z (Z blocks the path).
3. **Common effect (v-structure):** X → Z ← Y — X and Y become *dependent* when Z or its descendant is observed ("explaining away").

**Bayes Ball algorithm / d-separation:** Path from X to Y is **blocked** given evidence E if:
- It passes through a chain or fork node in E, OR
- It passes through a v-structure where neither Z nor any of Z's descendants are in E.

## Exact Inference in Bayesian Networks

### Inference by Enumeration
- Query: P(X | e) = α Σ_hidden P(X, e, hidden)
- Sum over all hidden variable combinations.
- **Exponential** in the number of hidden variables.

### Variable Elimination
- Eliminate hidden variables one by one by summing out (marginalization).
- Cache intermediate factors to avoid redundant computation.
- **Complexity:** Exponential in the **treewidth** of the network, polynomial for singly connected (polytree) networks.

### Polytree Algorithm (Belief Propagation)
- Exact inference for singly connected networks (no undirected cycles).
- Messages pass from leaves inward, then outward.
- **Linear time** in the number of variables.

### Junction Tree Algorithm (Clique Tree Propagation)
- Exact inference for arbitrary networks.
- Construct a tree of cliques; run belief propagation on the tree.
- Exponential in the size of the largest clique (which equals treewidth + 1).
- **Exact but expensive** for dense networks.

## Approximate Inference: Sampling Methods

### Direct Sampling
- Generate samples from the joint distribution using the network's topological order.
- Estimate P(query) from the frequency of matching samples.

### Rejection Sampling
- Generate samples; reject those inconsistent with evidence; estimate from remaining.
- **Inefficient** when evidence has low probability.

### Likelihood Weighting
- Fix evidence variables; sample only non-evidence variables.
- Weight each sample by the likelihood of the evidence: w = ∏ P(eᵢ | Parents(eᵢ)).
- **Consistent** estimator; more efficient than rejection sampling.

### Markov Chain Monte Carlo (MCMC)
- Generate a sequence of samples via a Markov chain that has the target distribution as its stationary distribution.
- **Gibbs sampling:** Sample each variable in turn from its distribution given all others (its Markov blanket). Very effective for Bayesian networks.
- **Metropolis-Hastings:** General MCMC method with acceptance/rejection step.
- Converges to correct distribution; mixing time may be slow for highly correlated variables.

## Other Probabilistic Models

### Naive Bayes Classifier
- Assumes all features Fᵢ are conditionally independent given the class C.
- P(C | f₁, ..., fₙ) ∝ P(C) ∏ᵢ P(fᵢ | C)
- Simple, fast, effective in practice (text classification, spam filtering).
- **Naïve** because independence assumption rarely holds exactly.

### Causal Networks
- Bayesian networks with causal interpretations.
- **Intervention (do-calculus):** P(Y | do(X=x)) ≠ P(Y | X=x) in general.
- **Pearl's do-calculus:** Formal framework for causal inference from observational data.

## Key Terms

- **Bayesian network:** DAG with CPTs representing a compact joint distribution.
- **CPT:** Conditional Probability Table — P(Xᵢ | Parents(Xᵢ)).
- **d-separation:** Graphical test for conditional independence in a BN.
- **Variable elimination:** Exact inference by marginalizing out hidden variables one at a time.
- **Likelihood weighting:** Weighted sampling algorithm for approximate inference.
- **Gibbs sampling:** MCMC method; samples each variable given its Markov blanket.
- **Markov blanket:** Parents, children, and co-parents of a node — sufficient to render it conditionally independent of all others.
- **Naive Bayes:** Classifier assuming features are conditionally independent given the class.
