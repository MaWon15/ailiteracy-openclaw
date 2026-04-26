# Chapter 4: Search in Complex Environments
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Beyond Classical Search

Classical search assumes fully observable, deterministic, known environments. Chapter 4 relaxes these assumptions:
- **Local search:** When the path doesn't matter, only the goal state.
- **Nondeterministic environments:** Actions may have multiple outcomes.
- **Partially observable environments:** Agent has incomplete knowledge of state.
- **Unknown environments (exploration):** Agent must discover the environment.

## Local Search Algorithms

Used when the **goal state itself** is the solution (not the path to it). Operate on a single "current" state and move to neighbors.

**Advantages:** Use very little memory; can find good solutions in very large continuous spaces.

### Hill-Climbing Search (Gradient Ascent/Descent)
- Move to the neighbor with the highest value (steepest ascent).
- **Problem: Gets stuck at:**
  - **Local maxima:** Peak that isn't the global maximum.
  - **Ridges:** Sequences of local maxima.
  - **Plateaus / flat maxima:** No uphill moves exist.
- **Stochastic hill-climbing:** Choose randomly among uphill moves.
- **Random-restart hill-climbing:** Restart from random states; trivially complete.
- **Sideways moves:** Allow moves to equal-valued neighbors (helps on shoulders, can loop on plateaus).

### Simulated Annealing
- Inspired by metallurgy: slowly "cool" the system.
- Accept worse moves with probability e^(ΔE/T), where T decreases over time.
- **Theorem:** If T decreases slowly enough, SA finds the global optimum with probability → 1.
- Tradeoff: cooling schedule affects quality vs. time.

### Beam Search
- Keep k states in parallel ("beams").
- At each step, generate all successors of k states, keep top-k by heuristic value.
- **Stochastic beam search:** Select k successors by probability proportional to value (less greedy).
- Not the same as k parallel hill-climbs — states communicate information.

### Genetic Algorithms
- Maintain a **population** of k individuals (states encoded as strings).
- Each iteration:
  1. **Selection:** Choose pairs proportional to fitness.
  2. **Crossover:** Combine substrings of two parents at a random **crossover point**.
  3. **Mutation:** Flip random bits with small probability.
- Combine features from successful states across the population.
- Useful when the state can be decomposed into independently useful parts.

### Local Search in Continuous Spaces
- **Gradient descent/ascent:** Move in direction of gradient ∇f(x).
- **Newton-Raphson:** Uses second derivatives (Hessian) for faster convergence.
- **Line search:** Find optimal step size along gradient direction.

## Searching with Nondeterministic Actions

When actions have uncertain outcomes, the agent must plan for contingencies.

- **AND-OR search trees:**
  - **OR nodes:** Agent chooses an action (choice).
  - **AND nodes:** Environment chooses an outcome (all outcomes must be handled).
- A **contingency plan** (conditional plan) handles any possible outcome.
- Solutions are **trees**, not sequences.

## Searching with Partial Observations

### Sensorless (Conformant) Problems
- Agent has no sensors — acts without perceiving.
- Maintains a **belief state**: set of possible physical states.
- Solution is a sequence of actions that achieves the goal in all possible states.
- Search is in **belief-state space**, not physical state space.

### Contingency Problems
- Agent has sensors but with limited information.
- Belief state updated using:
  - **Prediction:** How actions change belief state.
  - **Observation:** How percepts narrow down belief state.
- Use AND-OR search in belief-state space.

## Online Search and Unknown Environments

**Online search agent:** Interleaves computation and action — must act before full environment is known.

- **Exploration problem:** Discover the map while navigating it.
- **Online DFS:** Backtrack by physically reversing actions. Explores every reachable state, but may traverse each edge multiple times (not efficient).
- **LRTA* (Learning Real-Time A*):** Updates heuristic estimates as it explores. Converges to optimal paths over multiple trials.

**Competitive ratio:** Online algorithm's worst-case path cost vs. offline optimal. DFS may be exponentially worse than optimal.

## Key Terms

- **Local search:** Search in a space of complete states, no path tracking.
- **Local maximum:** A state that is better than all neighbors but not globally optimal.
- **Simulated annealing:** Probabilistically accepts worse moves to escape local maxima.
- **Genetic algorithm:** Population-based search using crossover and mutation.
- **Belief state:** The set of physical states consistent with the agent's observations.
- **AND-OR tree:** Search structure for nondeterministic actions — AND nodes for outcomes, OR nodes for choices.
- **Online search:** Agent acts in environment as it explores — no complete map available.
