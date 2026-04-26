# Chapter 12: Quantifying Uncertainty
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Why Uncertainty?

Agents operating in the real world face **partial observability** and **nondeterminism**. Logical agents with incomplete information face:
- **Laziness:** Impractical to list all conditions for every rule.
- **Ignorance:** Lack of knowledge about relevant facts.

**Probability theory** provides a formal framework for reasoning under uncertainty — summarizing all that is not known.

## Probability Basics

### Sample Space and Events
- **Sample space Ω:** Set of all possible worlds (outcomes).
- **Event:** A subset of Ω.
- **Probability function P:** Assigns real values to events satisfying:
  1. 0 ≤ P(ω) ≤ 1 for all ω ∈ Ω.
  2. Σ P(ω) = 1.

### Random Variables
- A function from outcomes to a range of values.
- **Discrete:** Boolean, multinomial (e.g., Weather ∈ {sunny, cloudy, rain}).
- **Continuous:** Real-valued (e.g., Temperature).

### Probability Distributions
- P(X = x): probability that random variable X takes value x.
- **Joint distribution:** P(X₁, X₂, ..., Xₙ) — probability of every combination.
- **Marginal distribution:** P(X) = Σ_y P(X, Y = y) — sum out other variables.

## Conditional Probability

**Definition:** P(A | B) = P(A ∧ B) / P(B), provided P(B) > 0.

**Product rule:** P(A ∧ B) = P(A | B) × P(B).

**Chain rule:** P(X₁ ∩ X₂ ∩ ... ∩ Xₙ) = ∏ᵢ P(Xᵢ | X₁, ..., Xᵢ₋₁).

## Bayes' Rule

**Bayes' Rule:** P(cause | effect) = P(effect | cause) × P(cause) / P(effect)

Equivalently: P(H | e) = P(e | H) × P(H) / P(e)

- **Prior P(H):** Belief before seeing evidence.
- **Likelihood P(e | H):** How probable is the evidence given the hypothesis?
- **Posterior P(H | e):** Updated belief after evidence.
- **Normalizing constant P(e) = α:** Ensures probabilities sum to 1.

**Bayes' Rule with multiple causes:** Used in naïve Bayes classifiers and diagnostic systems.

## Independence and Conditional Independence

**Independence:** P(X | Y) = P(X), equivalently P(X, Y) = P(X) × P(Y).

**Conditional independence:** P(X | Y, Z) = P(X | Z) — X and Y are independent given Z.
- Example: Cavity ⊥ Weather (unconditional independence).
- Example: Toothache ⊥ Catch | Cavity (conditional independence given cavity).

Conditional independence is the key to compact probabilistic representations (Bayesian networks).

## The Full Joint Distribution

- Specifies P(x₁, ..., xₙ) for all combinations of values.
- For n binary variables: 2^n − 1 numbers needed.
- **Too large for practical use** in complex domains — motivates compact representations.

**Inference by enumeration:** To compute P(query | evidence), sum over hidden variables in the joint.

## Probability in Practice

### Frequentist vs. Bayesian Interpretations
- **Frequentist:** Probability = long-run frequency of events.
- **Bayesian (subjective):** Probability = degree of belief; updated via Bayes' Rule.

### Calibration
A good probabilistic agent should be **calibrated** — among all events assigned probability p, approximately p of them actually occur.

### Decision-Making Under Uncertainty
- **Maximum Expected Utility (MEU):** Choose action a* = argmax_a Σ_s P(s | a) × U(s).
- Combines probability (beliefs) with utility (preferences).

## Distributions Over Continuous Variables

- **Probability density function (PDF):** P(X = x) as a continuous function; probabilities are integrals.
- **Gaussian (Normal) distribution:** N(μ, σ²) — bell curve; parameterized by mean and variance.
- **Multivariate Gaussian:** Extends to multiple variables with mean vector and covariance matrix.
- Gaussian is closed under conditioning and marginalization — critical for Kalman filters.

## Key Terms

- **Prior probability P(H):** Probability before observing evidence.
- **Posterior probability P(H|e):** Probability updated after observing evidence e.
- **Bayes' Rule:** Relates prior, likelihood, and posterior.
- **Conditional independence:** X ⊥ Y | Z — X and Y are independent given Z.
- **Joint probability distribution:** Probability of every combination of variable values.
- **Marginal distribution:** Distribution of a subset of variables (obtained by summing/integrating out others).
- **Maximum Expected Utility (MEU):** Choose the action that maximizes expected utility.
