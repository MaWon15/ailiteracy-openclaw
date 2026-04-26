# Chapter 3: Solving Problems by Searching
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Problem-Solving Agents

A **goal-based agent** formulates goals and searches for action sequences that achieve them. This requires:
- A clearly defined goal state.
- A formal problem representation.
- A search algorithm to find a solution.

**Assumption:** The environment is fully observable, discrete, known, and deterministic (single-agent).

## Problem Formulation

A problem is defined by five components:
1. **Initial state** — where the agent starts.
2. **Actions(s)** — set of actions available in state *s*.
3. **Transition model** — Result(s, a) = s′; describes what each action does.
4. **Goal test** — determines whether a given state is a goal state.
5. **Path cost** — assigns a numeric cost to each path; step cost c(s, a, s′).

The **state space** is the set of all states reachable from the initial state. Represented as a graph: nodes = states, edges = actions.

A **solution** is a sequence of actions leading from the initial state to a goal state. An **optimal solution** has the lowest path cost.

## Search Algorithms

A **search tree** is built by expanding nodes. Each node contains:
- State, parent node, action taken, path cost g(n), depth.

**The frontier** (open list): nodes generated but not yet expanded.
**Explored set** (closed list): nodes already expanded.

## Uninformed (Blind) Search Strategies

No information about the distance to the goal beyond problem definition.

### Breadth-First Search (BFS)
- Expands shallowest unexpanded node.
- Uses a FIFO queue as frontier.
- **Complete:** Yes (if branching factor *b* is finite).
- **Optimal:** Yes, if step costs are equal.
- **Time:** O(b^d) — exponential in depth *d*.
- **Space:** O(b^d) — keeps all nodes in memory.

### Uniform-Cost Search (UCS / Dijkstra's)
- Expands node with lowest path cost g(n).
- Uses a priority queue.
- **Complete:** Yes (if step costs > ε > 0).
- **Optimal:** Yes.
- **Time/Space:** O(b^(1+⌊C*/ε⌋)) where C* is optimal cost.

### Depth-First Search (DFS)
- Expands deepest unexpanded node.
- Uses a LIFO stack (or recursion).
- **Complete:** No (fails in infinite spaces; yes for finite acyclic graphs).
- **Optimal:** No.
- **Time:** O(b^m) — depends on max depth *m*.
- **Space:** O(bm) — linear in depth (major advantage).

### Depth-Limited Search
- DFS with a predetermined depth limit *l*.
- Solves DFS's infinite loop problem but introduces incompleteness if *l < d*.

### Iterative Deepening Search (IDS)
- Repeatedly applies depth-limited search with increasing limits (0, 1, 2, ...).
- **Complete:** Yes.
- **Optimal:** Yes (uniform step costs).
- **Time:** O(b^d) — same asymptotic as BFS.
- **Space:** O(bd) — linear like DFS. Best uninformed strategy in practice.

### Bidirectional Search
- Simultaneously searches forward from start and backward from goal.
- Searches meet in the middle.
- **Time/Space:** O(b^(d/2)) — significant speedup.

## Informed (Heuristic) Search Strategies

Use **heuristic function** h(n) = estimated cost to reach the goal from node *n*.

**Admissible heuristic:** h(n) ≤ h*(n) (never overestimates the true cost). Required for A* optimality in tree search.
**Consistent (monotone) heuristic:** h(n) ≤ c(n, a, n′) + h(n′). Guarantees A* optimality in graph search.

### Greedy Best-First Search
- Expands node with lowest h(n).
- Not optimal, not complete (can get stuck in loops).
- Fast but suboptimal.

### A* Search
- Expands node with lowest f(n) = g(n) + h(n).
- g(n) = cost from start to *n*; h(n) = estimated cost from *n* to goal.
- **Complete:** Yes.
- **Optimal:** Yes, if h is admissible (tree search) or consistent (graph search).
- **Optimally efficient:** No other optimal algorithm expands fewer nodes (given same heuristic).
- **Space:** Exponential — keeps all nodes in memory (main weakness).

### Weighted A*
- f(n) = g(n) + W·h(n) with W > 1.
- Faster but trades optimality for speed (ε-optimal: cost ≤ W × optimal).

### Memory-Bounded Heuristic Search
- **IDA*:** Iterative deepening A* using f-cost threshold. Linear memory, optimal.
- **RBFS:** Recursive Best-First Search — linear memory, optimal, but can re-expand nodes.
- **SMA*:** Simplified Memory-Bounded A* — uses available memory efficiently.

## Heuristic Design

**Relaxed problems:** Derive admissible heuristics by relaxing constraints.
- 8-puzzle: h1 = number of misplaced tiles; h2 = sum of Manhattan distances.
- h2 dominates h1 (h2(n) ≥ h1(n) for all n) — always prefer the higher admissible heuristic.

**Pattern databases:** Store exact costs for subproblems; combine for lower bounds.

**Effective branching factor b*:** A measure of heuristic quality. Well-designed heuristics achieve b* close to 1.

## Key Terms

- **Completeness:** Guaranteed to find a solution if one exists.
- **Optimality:** Guaranteed to find the least-cost solution.
- **Heuristic function h(n):** Estimate of cost from node *n* to goal.
- **Admissible heuristic:** Never overestimates the true cost.
- **A* search:** Optimal and complete informed search using f = g + h.
