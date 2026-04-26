# Chapter 11: Automated Planning
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is Planning?

**Planning** is the process of generating a sequence of actions to achieve a goal from an initial state.

**Classical planning assumptions:**
- Fully observable, deterministic, static, discrete, single-agent environment.
- Actions have deterministic effects described by preconditions and effects.

Planning improves over search by using **factored state representation** (explicit features), enabling more powerful inference.

## The Planning Domain Definition Language (PDDL)

PDDL is the standard language for specifying planning problems.

### State Representation
- States are sets of ground atoms (closed-world assumption).
- Example: At(Plane1, JFK) ∧ At(Plane2, SFO) ∧ In(Cargo1, Plane1)

### Action Schemas
Each action is defined by:
- **Name and parameters:** Load(cargo, plane, airport)
- **Precondition:** Conditions that must hold (conjunction of literals).
- **Effect:** Changes to the state (conjunction of positive/negative literals).

Example (Air Cargo):
```
Action(Load(c, p, a),
  PRECOND: At(c, a) ∧ At(p, a) ∧ Cargo(c) ∧ Plane(p) ∧ Airport(a)
  EFFECT: ¬At(c, a) ∧ In(c, p))
```

### Plan Semantics
- **Applicable action:** Precondition is satisfied in current state.
- **Result state:** Add positive effects, remove negated effects (**STRIPS assumption** — only changed atoms listed).
- **Frame assumption:** Anything not mentioned in effects stays unchanged.

## Planning as Search

### Forward State-Space Search
- Start from initial state; apply applicable actions; search for goal state.
- Uses heuristics derived from relaxed planning problems.

### Backward (Regression) Search
- Start from goal; work backward: what states could lead to the goal?
- **Relevant action:** An action is relevant if it achieves at least one goal literal.
- **Consistent action:** Applying action backward doesn't negate a goal literal.

### Planning Heuristics
- **Ignore-preconditions heuristic:** Drop all preconditions — every action always applies. Optimal cost of relaxed problem is a lower bound.
- **Ignore-delete-lists heuristic:** Remove all negative effects — monotonically grow state. Solvable in polynomial time with greedy search.
- **Pattern databases:** Pre-compute costs for subgoals.
- **Additive heuristic:** Sum independent subgoal estimates (inadmissible but effective).
- **Max heuristic:** Maximum of independent subgoal estimates (admissible).

## The Planning Graph

A **planning graph** is a polynomial-time structure used to compute good heuristics.

Structure (alternating layers):
- **State layers (Sᵢ):** Sets of literals that might hold.
- **Action layers (Aᵢ):** Actions whose preconditions appear in Sᵢ.

**Mutex (mutual exclusion) relations:**
- **Action mutex:** Two actions that conflict (one negates the other's precondition/effect, or they compete for same precondition).
- **Literal mutex:** Two literals that cannot both be true (one negates the other, or all ways to achieve them are mutex).

**Level cost:** Earliest layer at which a goal literal first appears, not mutex with all other goals.

**GRAPHPLAN:** Directly extracts a plan from the planning graph if one exists; otherwise extends the graph.

### FF (Fast Forward) Planner
- Uses ignore-delete-lists heuristic computed via planning graph.
- Enforced hill-climbing: if current state has no neighbors closer to goal, backtrack.
- One of the most successful classical planners.

## Other Planning Approaches

### SAT-Based Planning (SATPLAN)
- Encode planning problem as SAT: propositions = "action a occurs at step t."
- Use a SAT solver; return the satisfying assignment as a plan.
- Very effective for bounded-horizon planning.

### Partial-Order Planning (POP)
- Plans as partial orders over actions rather than strict sequences.
- **Least commitment:** Only add constraints when needed.
- Handles **causal links** and **threats** (actions that could undo earlier effects).
- Supports more flexible parallel planning.

## Planning with Uncertainty

### Conditional Planning (Contingent Planning)
- Use sensing actions to gather information during execution.
- Plan is a tree (AND-OR structure), not a sequence.

### Replanning
- Plan optimistically; monitor execution; replan if unexpected events occur.

### MDPs and Policies (see Chapter 17)
- When environment is stochastic, the optimal solution is a policy π: state → action.

## Hierarchical Planning (HTN)

**Hierarchical Task Networks (HTN):**
- Plans are defined in terms of **tasks** that decompose into sub-tasks.
- **Primitive tasks:** Directly executable actions.
- **Non-primitive tasks:** Must be decomposed via **methods**.
- Encodes domain knowledge about how to solve problems (expert knowledge).
- More expressive and practical for real-world planning (SHOP2, HTN planners).

## Multi-Agent Planning

- **Decentralized planning:** Each agent plans independently; joint plan must be coordinated.
- **Cooperative vs. competitive agents.**
- **Joint actions:** Multiple agents act simultaneously; effects depend on combined actions.
- Communication and coordination are key challenges.

## Key Terms

- **PDDL:** Planning Domain Definition Language — standard for expressing planning problems.
- **STRIPS assumption:** Only effects listed in an action change the state.
- **Planning graph:** Level-based structure used to compute heuristics and find plans.
- **Mutex:** Mutual exclusion — two literals/actions that cannot coexist.
- **HTN planning:** Hierarchical decomposition of tasks using domain-specific methods.
- **Partial-order planning:** Represents plans as partial orders to allow flexible scheduling.
- **Replanning:** Execute, monitor, and replan when the world deviates from expectations.
