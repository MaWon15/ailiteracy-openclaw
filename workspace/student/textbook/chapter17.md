# Chapter 17: Making Complex Decisions
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Sequential Decision Problems

When decisions must be made over time and actions affect future states, we need **sequential decision theory**.

**Markov Decision Process (MDP):** The standard model for sequential decision making under uncertainty.

## Markov Decision Processes (MDPs)

### Components
- **States S:** Set of possible world states.
- **Actions A:** Set of available actions.
- **Transition model P(s′ | s, a):** Probability of reaching state s′ from state s with action a.
- **Reward function R(s, a, s′) or R(s):** Immediate reward received.
- **Discount factor γ ∈ [0, 1]:** Weight on future rewards.
- **Initial state distribution.**

### Policies
A **policy** π: S → A specifies which action to take in each state.
- **Optimal policy π*:** Maximizes expected utility (total discounted reward) from any state.

### Utility of Sequences
**Total discounted reward** starting from state s₀:  
U(s₀, s₁, ...) = R(s₀) + γR(s₁) + γ²R(s₂) + ... = Σₜ γᵗ R(sₜ)

Discounting ensures bounded utility for infinite horizons (when γ < 1).

### Horizon
- **Finite horizon:** Fixed number of steps; optimal policy may be non-stationary (depends on time).
- **Infinite horizon:** No fixed endpoint; optimal policy is **stationary** (time-independent).

## Value Functions and Bellman Equations

### Value Function
V*(s) = expected utility starting from state s and acting optimally.

### Bellman Equation (optimality condition):
V*(s) = max_a Σ_{s′} P(s′ | s, a) [R(s, a, s′) + γ V*(s′)]

- The value of a state is the maximum over actions of: immediate reward + discounted expected value of next state.

### Q-values (Action-Value Function)
Q*(s, a) = Σ_{s′} P(s′ | s, a) [R(s, a, s′) + γ V*(s′)]
V*(s) = max_a Q*(s, a)

## Value Iteration

**Algorithm:**
1. Initialize V(s) = 0 for all s.
2. Repeat: V(s) ← max_a Σ_{s′} P(s′|s,a) [R(s,a,s′) + γV(s′)] for all s.
3. Until max |V_new(s) − V_old(s)| < ε (convergence).

- **Convergence:** Guaranteed for γ < 1 (contraction mapping).
- **Complexity per iteration:** O(|S|² × |A|).
- Typically converges in tens to hundreds of iterations.

## Policy Iteration

1. Initialize π arbitrarily.
2. **Policy evaluation:** Compute V^π (solve linear system or iterate).
3. **Policy improvement:** For each state, greedy action = argmax_a Σ P [R + γV^π].
4. If policy changed, go to 2; else return π.

- **Convergence:** Guaranteed in finite steps (at most |A|^|S| policies).
- Often converges in fewer iterations than value iteration.

## Partially Observable MDPs (POMDPs)

When the agent **cannot observe the true state** directly:
- Agent maintains a **belief state** b(s) = P(s | observations so far).
- **Belief MDP:** The belief state itself is the state; transitions via Bayes' rule.
- POMDP optimal policy maps belief states to actions.

### POMDP Value Function
- V*(b) is a **piecewise-linear convex function** of the belief state.
- Represented as a set of α-vectors (one per action/history).
- **Value iteration for POMDPs (Perseus, PBVI):** Compute upper/lower bounds on V*.
- **Approximate methods:** Point-based value iteration, online planning (POMCP).

**Applications:** Dialogue systems, robot navigation under uncertainty, medical treatment planning.

## Decisions with Multiple Agents

### Game Theory (Normal Form)
- **Strategy:** Complete specification of what to do in every situation.
- **Pure strategy:** Deterministic choice.
- **Mixed strategy:** Probability distribution over pure strategies.

### Nash Equilibrium
A strategy profile (σ₁, ..., σₙ) is a **Nash equilibrium** if no agent can unilaterally increase its utility by changing its strategy:  
∀i: σᵢ is a best response to σ₋ᵢ.

**Nash's theorem (1950):** Every finite game has at least one Nash equilibrium (possibly in mixed strategies).

### Dominant Strategies
- **Strictly dominant:** Always better than any other strategy, regardless of opponents' play.
- **Iterated elimination of dominated strategies (IEDS):** Remove dominated strategies repeatedly; may simplify or solve the game.

### Prisoner's Dilemma
- **Cooperate/Defect:** Defection is strictly dominant for both players, yet mutual defection is worse for both than mutual cooperation.
- Illustrates tension between individual rationality and collective welfare.
- **Repeated games:** Cooperation can emerge as a Nash equilibrium (Tit-for-Tat strategy).

### Mechanism Design (Inverse Game Theory)
- Design rules of the game such that agents acting in their self-interest produce a desired outcome.
- **Vickrey-Clarke-Groves (VCG) mechanism:** Implements socially optimal outcomes with dominant-strategy truthfulness.
- Applications: auctions, voting, resource allocation.

## Multiagent Reinforcement Learning
- Multiple agents learn simultaneously; environment includes other learning agents.
- **Non-stationarity:** Each agent's environment changes as others learn.
- **Cooperative:** Agents share a reward function (team MARL).
- **Competitive:** Zero-sum games.
- **Mixed motives:** Combination of cooperation and competition.

## Key Terms

- **MDP:** Markov Decision Process — sequential decision making under uncertainty.
- **Policy π:** Mapping from states to actions.
- **Value function V*(s):** Expected utility of acting optimally from state s.
- **Bellman equation:** Recursive definition of optimal value function.
- **Value iteration:** Algorithm for computing V* via repeated Bellman backups.
- **Policy iteration:** Alternate policy evaluation and improvement until convergence.
- **POMDP:** MDP with partial observability; agent maintains a belief state.
- **Nash equilibrium:** No agent can unilaterally improve by deviating.
- **Mechanism design:** Design game rules to align individual incentives with desired outcomes.
