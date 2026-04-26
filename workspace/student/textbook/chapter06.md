# Chapter 6: Constraint Satisfaction Problems
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is a CSP?

A **Constraint Satisfaction Problem (CSP)** is defined by:
- **Variables:** X = {X₁, X₂, ..., Xₙ}
- **Domains:** D = {D₁, D₂, ..., Dₙ} — possible values for each variable.
- **Constraints:** C = {C₁, C₂, ..., Cₘ} — allowable combinations of variable values.

A **solution** is a complete assignment of values to variables such that all constraints are satisfied.

**Advantages over standard search:** CSP solvers exploit problem structure; constraint propagation eliminates large portions of the search space early.

**Examples:** Map coloring, Sudoku, 8-queens, scheduling, circuit layout, timetabling.

## Constraint Types

- **Unary constraint:** Restricts a single variable. (e.g., SA ≠ green)
- **Binary constraint:** Relates two variables. (e.g., SA ≠ WA)
- **Higher-order constraint:** Involves 3+ variables.
- **Global constraint:** Involves an arbitrary number of variables. (e.g., Alldiff, Alldifferent)
- **Soft constraint (preference):** Preferred but not required — used in **constraint optimization problems**.

Any finite-domain CSP can be converted to binary CSP by introducing auxiliary variables.

## Constraint Propagation

**Inference:** Uses constraints to reduce domains of variables before or during search.

### Node Consistency (NC)
- All values in a variable's domain satisfy its unary constraints.

### Arc Consistency (AC-3)
- Variable Xᵢ is arc-consistent with Xⱼ if for every value in Dᵢ there is some consistent value in Dⱼ.
- **AC-3 algorithm:** Maintains a queue of arcs; removes inconsistent values; re-adds affected arcs.
- **Complexity:** O(cd³) where c = number of constraints, d = domain size.
- Does not guarantee a solution — only reduces domains.

### Path Consistency (PC) and k-Consistency
- Path consistency: every consistent assignment of two variables can be extended to a third.
- k-consistency: any consistent assignment of k-1 variables can be extended to a k-th.
- Strong k-consistency (k and all lower levels) → can solve without backtracking.

## Backtracking Search for CSPs

Depth-first search where one variable is assigned at a time; backtracks when no legal value exists.

### Variable Ordering Heuristics
- **MRV (Minimum Remaining Values):** Choose the variable with the fewest legal values ("fail-first"). Reduces branching.
- **Degree heuristic:** Among MRV ties, choose the variable with the most constraints on unassigned variables.

### Value Ordering Heuristics
- **LCV (Least Constraining Value):** Assign the value that rules out the fewest choices for neighboring variables. "Fail-last" — try to succeed.

### Inference During Search
- **Forward checking:** After assigning Xᵢ, check each unassigned neighbor; remove inconsistent values. Detects failure early.
- **MAC (Maintaining Arc Consistency):** Run AC-3 after each assignment. More powerful than forward checking.

### Backjumping
- **Chronological backtracking:** Returns to most recent variable (standard DFS).
- **Backjumping:** Jump back to the conflicting variable (the one responsible for the failure).
- **Conflict-directed backjumping (CBJ):** Jumps to the deepest variable in the conflict set.

### Constraint Learning (No-good recording)
- Record **no-goods** (sets of assignments that lead to dead ends) to avoid repeating them.
- **Conflict-directed backjumping + constraint learning** = most effective approach.

## Local Search for CSPs

Start with a complete assignment (possibly violating constraints); repair violations.

- **Min-conflicts heuristic:** Choose the value for the current variable that violates the fewest constraints.
- Very effective in practice (solves million-queen problems in constant average time).
- Does not guarantee a solution (can get stuck).

## Problem Structure

Exploiting the structure of the constraint graph can dramatically speed up solving.

- **Independent subproblems:** If the constraint graph has multiple connected components, solve independently. Reduces from O(d^n) to O(n/c × d^c) for c-size components.
- **Tree-structured CSPs:** If the constraint graph is a tree (no cycles), solvable in O(nd²) time using directed arc consistency — no backtracking needed.
- **Cutset conditioning:** Find a small **cycle cutset** (variables whose removal makes the graph a tree). Try all assignments of cutset variables; solve remaining tree-structured CSP. Size c cutset → O(d^c × nd²).
- **Tree decomposition:** Decompose into subproblems arranged in a tree; **treewidth** w → O(nd^(w+1)).

## Key Terms

- **CSP:** Problem with variables, domains, and constraints.
- **Arc consistency (AC-3):** Ensures each domain value has a consistent neighbor value.
- **Backtracking search:** DFS assigning one variable at a time, with inference and heuristics.
- **MRV:** Minimum Remaining Values — choose most constrained variable first.
- **LCV:** Least Constraining Value — choose value that restricts neighbors least.
- **Forward checking:** Propagate constraints after each assignment to detect failure early.
- **Min-conflicts:** Local search heuristic for CSPs; very effective in practice.
- **Treewidth:** Measure of graph structure; low treewidth → efficient solving.
