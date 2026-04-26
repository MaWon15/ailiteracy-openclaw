# Chapter 5: Adversarial Search and Games
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Games as Search Problems

**Games** are multiagent environments where agents have conflicting goals. AIMA focuses on:
- **Deterministic, fully observable, two-player, zero-sum games** (perfect information).
- Examples: Chess, checkers, Go, tic-tac-toe.

**Formal definition:**
- **S₀:** Initial state.
- **To-Move(s):** Which player moves in state *s*.
- **Actions(s):** Legal moves in state *s*.
- **Result(s, a):** Transition model.
- **Is-Terminal(s):** Terminal test.
- **Utility(s, p):** Numerical value for player *p* in terminal state *s* (e.g., +1 win, 0 draw, –1 loss).

**Game tree:** Entire search space of a game.

## Minimax Search

- **MAX player** tries to maximize utility; **MIN player** tries to minimize it.
- **Minimax value** of a node: the utility for MAX assuming both players play optimally.
  - MAX node: minimax(s) = max over actions of minimax(Result(s,a))
  - MIN node: minimax(s) = min over actions of minimax(Result(s,a))
  - Terminal: minimax(s) = Utility(s)

- **Complete:** Yes (in finite game trees).
- **Optimal:** Yes (against an optimal opponent).
- **Time:** O(b^m) — exponential.
- **Space:** O(bm) — linear (depth-first).

## Alpha-Beta Pruning

Prunes branches that cannot affect the final decision — same result as minimax but faster.

- **α (alpha):** Best value MAX can guarantee along current path (initially –∞).
- **β (beta):** Best value MIN can guarantee along current path (initially +∞).
- **Prune a MIN node** when its value ≤ α (MAX won't choose this path).
- **Prune a MAX node** when its value ≥ β (MIN won't allow this path).

**Complexity:**
- Perfect ordering: O(b^(m/2)) — effectively doubles the search depth.
- Random ordering: O(b^(3m/4)).
- **Move ordering** (best moves first) dramatically improves pruning effectiveness.

## Imperfect Real-Time Decisions

Real games (chess, Go) have search trees too large for exhaustive minimax.

### Heuristic Cutoff
- Replace terminal-test with a **cutoff test** (depth limit or time limit).
- Replace Utility with an **evaluation function** h(s, p) estimating the state's value.
- Evaluation functions: weighted sum of features (material, position, king safety, etc.).
- **Quiescence search:** Continue searching beyond cutoff in "volatile" positions to avoid horizon effect.
- **Horizon effect:** Agent overlooks threats just beyond its search depth.
- **Singular extension:** Extend search on forced/clearly best moves.

### Forward Pruning
- **Beam search in games:** Consider only best k moves at each ply.
- **ProbCut:** Probabilistically prune moves unlikely to affect the outcome.
- Risk: May prune the best move.

### Transposition Tables
- Hash table storing previously evaluated positions.
- Avoids re-evaluating transpositions (same position reached via different move sequences).
- **Zobrist hashing** is a common efficient technique.

## Monte Carlo Tree Search (MCTS)

Does not require an evaluation function — estimates value through **simulations** (playouts).

**Four phases per iteration:**
1. **Selection:** Traverse tree using a policy (e.g., UCB1) until a leaf node.
2. **Expansion:** Add one or more child nodes.
3. **Simulation (Rollout):** Play randomly to a terminal state.
4. **Backpropagation:** Update win/visit counts along the path.

**UCB1 (Upper Confidence Bound):**  
UCB1(n) = wins(n)/visits(n) + C × √(ln(visits(parent))/visits(n))
- Balances exploitation (high win rate) and exploration (few visits).

**AlphaGo / AlphaZero:** MCTS guided by deep neural networks for both policy (move probabilities) and value (position evaluation). Defeated world champions in Go (2016–2017).

## Stochastic Games

Environments with chance elements (dice, cards).

- Add **chance nodes** to the game tree (expectiminimax).
- **Expected minimax value** weights minimax values by outcome probabilities.
- **Backgammon:** Stochastic game; TD-Gammon learned to play at expert level via self-play + temporal difference learning.

## Partially Observable Games (Imperfect Information)

- **Card games (Poker, Bridge):** Hidden information about opponents' hands.
- Approach: enumerate possible states consistent with observations, compute probabilities, choose action with highest expected utility.
- **Counterfactual regret minimization (CFR):** State-of-the-art for large imperfect-information games (Libratus, Pluribus defeated professional poker players).

## Key Terms

- **Minimax:** Optimal strategy assuming both players play optimally in zero-sum games.
- **Alpha-beta pruning:** Eliminates branches that cannot influence the minimax decision.
- **Evaluation function:** Heuristic estimate of state value used for cutoff decisions.
- **MCTS:** Simulation-based search; effective without an evaluation function.
- **Horizon effect:** Misguided action due to threats just beyond the search depth limit.
- **Transposition table:** Cache of previously evaluated positions to avoid redundant search.
