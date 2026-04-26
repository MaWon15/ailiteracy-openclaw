# Chapter 18: Multiagent Decision Making
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Why Multiagent Systems?

Many real-world AI deployments involve **multiple agents** — autonomous programs that interact:
- Markets, auctions, trading platforms.
- Autonomous vehicles at intersections.
- Networked robots in warehouses.
- AI systems negotiating on behalf of humans.

Agents may be **cooperative** (aligned goals), **competitive** (opposing goals), or **mixed-motive**.

## Properties of Multiagent Environments

- **Competitive vs. cooperative.**
- **Simultaneous vs. sequential decisions.**
- **Observable vs. partially observable** (what does each agent know?).
- **Communication allowed?** (cheap talk vs. binding commitments).
- **Self-interested vs. benevolent agents.**

## Social Choice and Voting

When agents must aggregate preferences into a collective decision:

### Voting Procedures
- **Plurality:** Most first-place votes wins.
- **Condorcet winner:** Beats every other candidate in pairwise comparisons (may not exist).
- **Borda count:** Each candidate gets points based on rank position.
- **Instant runoff (IRV):** Eliminate last-place candidates iteratively.

### Arrow's Impossibility Theorem (1951)
No voting procedure for 3+ candidates satisfies all of:
1. **Pareto efficiency:** If all prefer A to B, A wins.
2. **Independence of irrelevant alternatives (IIA):** The ranking of A vs. B depends only on voters' relative rankings of A and B.
3. **Non-dictatorship:** No single voter determines the outcome.

This theorem is fundamental — it means every voting system has some flaw.

### Gibbard-Satterthwaite Theorem
Any non-dictatorial voting procedure for 3+ outcomes is susceptible to **strategic voting** (manipulation).

## Mechanism Design

**Goal:** Design rules of the game so that when self-interested agents act optimally, the collective outcome is desirable.

### Incentive Compatibility
A mechanism is **incentive compatible** (IC) if truthful reporting is a dominant strategy for each agent.

### Auctions
**First-price sealed-bid:** Highest bidder wins and pays their bid.
- Bidders shade their bids below true value.

**Second-price sealed-bid (Vickrey auction):**
- Highest bidder wins and pays the *second-highest* bid.
- **Truth-telling is a dominant strategy** — bidding true value is optimal regardless of others.
- Simple and efficient.

**English auction (ascending):** Bids rise until one bidder remains. Equivalent to Vickrey for independent private values.

**Dutch auction (descending):** Price falls until a bidder accepts.

**Combinatorial auctions:** Bidders bid on *bundles* of items (allows expression of complementarity and substitutability).
- **Winner determination is NP-hard.**
- VCG mechanism extends to combinatorial settings.

### VCG Mechanism
- Agents report valuations.
- Social welfare maximizing outcome is chosen.
- Each agent pays: the social welfare of others *without* the agent, minus the social welfare of others *with* the agent.
- **Dominant strategy: truthful reporting.**
- **Pareto efficient** and **individually rational**.

## Cooperative Game Theory

Agents form **coalitions** to achieve better outcomes collectively.

### Transferable Utility (TU) Games
- A coalition S has a **value v(S)** (total payoff it can guarantee).
- **Core:** Set of payoff distributions such that no coalition can profitably deviate.
- **Shapley value:** Fair distribution of total payoff based on each agent's marginal contribution.
  - Shapley value φᵢ = average marginal contribution of agent i over all orderings.
  - Satisfies: efficiency, symmetry, dummy player, additivity.

## Communication and Coordination

### Cheap Talk
- Communication that does not cost anything and has no binding commitment.
- Credible only when interests align (sender cannot benefit from lying).

### Correlated Equilibrium
- A distribution over strategy profiles such that following the "recommendation" is optimal for each agent (given others follow it).
- **Broader than Nash equilibrium** — includes Nash equilibria as special cases.
- Can be found in polynomial time (vs. Nash which is PPAD-hard).

### Commitment and Contracts
- Binding agreements allow cooperation in cases where cheap talk cannot.

## Multiagent Learning

Multiple agents learning simultaneously creates a **non-stationary environment** — each agent's optimal strategy shifts as others learn.

### Approaches
- **Minimax Q-learning:** For two-player zero-sum games.
- **Nash Q-learning:** Converges to Nash equilibria under limiting conditions.
- **Fictitious play:** Each agent best-responds to the empirical frequency of others' past actions.
- **Mean field approximation:** For large populations — treat others as a statistical field.

## Distributed Constraint Optimization (DCOP)

Multiagent generalization of CSPs:
- Variables distributed among agents.
- Constraints (costs) between agents.
- **Goal:** Find assignment minimizing total cost.
- Algorithms: ADOPT (asynchronous backtracking), DPOP (dynamic programming), DSA (stochastic local search).

## Key Terms

- **Mechanism design:** Design game rules to align self-interest with desired outcomes.
- **Vickrey auction:** Second-price auction; truth-telling is dominant strategy.
- **VCG mechanism:** Generalizes Vickrey to multi-item settings; efficient and IC.
- **Nash equilibrium:** No agent can unilaterally improve (Chapter 17 revisited in multiagent context).
- **Core:** Payoff distributions that no coalition can improve upon.
- **Shapley value:** Fair attribution of collective payoff based on marginal contributions.
- **Arrow's Impossibility Theorem:** No voting rule satisfies all desirable properties for 3+ candidates.
- **Correlated equilibrium:** Generalization of Nash equilibrium allowing correlated strategies.
