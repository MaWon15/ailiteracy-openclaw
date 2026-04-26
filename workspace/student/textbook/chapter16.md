# Chapter 16: Making Simple Decisions
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Decision Theory

**Decision theory** = probability theory + utility theory.

**Principle of Maximum Expected Utility (MEU):**  
A rational agent should choose the action that maximizes its expected utility.  
a* = argmax_a Σ_s P(Result(a) = s) × U(s)

This is both a **descriptive** theory (how rational agents behave) and a **normative** theory (how agents *should* behave).

## Utility Theory

### Preferences and Orders
- **Preference:** Agent prefers A to B, denoted A ≻ B.
- **Indifference:** Agent is indifferent between A and B, denoted A ~ B.
- **Lotteries:** Probability distributions over outcomes, e.g., [p, A; 1−p, B].

### Axioms of Utility Theory (von Neumann-Morgenstern)
For preferences to be representable by a utility function, they must satisfy:

1. **Orderability:** A ≻ B, B ≻ A, or A ~ B (no incomparability).
2. **Transitivity:** If A ≻ B and B ≻ C, then A ≻ C.
3. **Continuity:** If A ≻ B ≻ C, there exists p such that [p, A; 1−p, C] ~ B.
4. **Substitutability:** If A ~ B, then [p, A; 1−p, C] ~ [p, B; 1−p, C].
5. **Monotonicity:** If A ≻ B, then p > q iff [p, A; 1−p, B] ≻ [q, A; 1−q, B].
6. **Decomposability:** Compound lotteries can be reduced to simple ones.

**Theorem (vNM):** Any preferences satisfying these axioms can be represented by a utility function U such that U(A) > U(B) iff A ≻ B.

### Utility Functions
- Utility is **unique up to positive linear transformation** (like Fahrenheit vs. Celsius).
- Money ≠ utility: **diminishing marginal utility** — each additional dollar is worth less.
- **Risk aversion:** Prefer certain outcome to a lottery with the same expected monetary value.
  - E.g., prefer $400,000 certain to 50% chance of $1,000,000.
- **Risk neutral:** Linear utility = expected value maximizer.
- **Risk seeking:** Prefer the lottery.

### Expected Utility
EU(a | e) = Σ_s P(Result(a) = s | e) × U(s)

## Utility of Money

### Certainty Equivalent
The certain amount CE such that the agent is indifferent between CE and the lottery.

CE(L) is the certainty equivalent of lottery L.

**Risk premium** = Expected monetary value − Certainty equivalent (positive for risk-averse agents).

### Utility Elicitation
- Assign U(best) = 1, U(worst) = 0.
- For any outcome o, find p such that [p, best; 1−p, worst] ~ o. Then U(o) = p.
- Standard gamble method.

### Exponential Utility Function
U(x) = −e^(−x/R) where R is the **risk tolerance**.
- Convenient because the certainty equivalent can be computed in closed form.
- Often used in finance and economics.

## Decision Networks (Influence Diagrams)

**Decision network** = Bayesian network + action nodes + utility node.

Three types of nodes:
- **Chance nodes (circles):** Random variables with probability distributions.
- **Decision nodes (rectangles):** Actions the agent controls.
- **Utility nodes (diamonds):** Represent the utility function.

### Evaluation Algorithm
1. Set decision node to each possible action.
2. Compute posterior probabilities for all chance nodes given evidence and action.
3. Compute expected utility for each action.
4. Select action with maximum EU.

### Value of Information

**Value of Perfect Information (VPI):**
VPI(Eⱼ | e) = EU(best action after observing Eⱼ) − EU(best action without Eⱼ)
= [Σ_{eⱼ} P(Eⱼ = eⱼ | e) × EU(best action | e, eⱼ)] − EU(best action | e)

Properties:
- VPI ≥ 0 always (information cannot hurt an optimal agent).
- VPI = 0 when the information doesn't change the optimal action.
- Information is worth acquiring only if VPI > cost of acquisition.
- **Non-additive** in general (the value of two pieces of info ≠ sum of individual VPIs).

## Multi-Attribute Utility Functions

Real decisions involve multiple objectives (cost, time, safety, comfort).

### Dominance
- **Strict dominance:** Option A dominates B if A is better on all attributes.
- **Stochastic dominance:** A stochastically dominates B if P(Utility(A) ≥ u) ≥ P(Utility(B) ≥ u) for all u.

### Additive Utility Functions
If attributes are **preferentially independent**:
U(x₁, ..., xₙ) = Σᵢ wᵢ × Uᵢ(xᵢ)

- Each attribute has its own utility function.
- Weighted sum of individual utilities.
- Tractable and commonly used in practice.

### Multiplicative Utility Functions
Used when attributes are not preferentially independent but satisfy **utility independence**:
U(x₁, ..., xₙ) = k⁻¹ [∏ᵢ (k wᵢ Uᵢ(xᵢ) + 1) − 1]

## Key Terms

- **Maximum Expected Utility (MEU):** Rational agents choose actions maximizing expected utility.
- **Utility function:** Represents agent preferences; unique up to positive linear transformation.
- **Lottery:** A probability distribution over outcomes.
- **Risk aversion:** Preference for certainty over a lottery with the same expected value.
- **Certainty equivalent:** The certain value equivalent in preference to a lottery.
- **Decision network (influence diagram):** BN extended with decision and utility nodes.
- **Value of Perfect Information (VPI):** Expected utility gain from learning a variable's value before acting.
