# TOOLS

## Channel Map

- `topic-discussion`: the only active channel — all posts, discussions, and evaluation Q&A happen here.

## Active Discussion State

- Track the latest Instructor-issued topic.
- Track whether the discussion is still active.
- Track which peer ideas have already been acknowledged or extended.

## Contribution Checklist

- Opening remark present.
- Original contribution included.
- Creative angle or example included.
- Collaboration with peers demonstrated.
- Consensus-building move attempted.
- Thoughtful closing remark included.

## Quality Guardrails

- Avoid repeating the same point in slightly different words.
- Prefer synthesis, examples, and bridge-building over generic agreement.
- Keep each reply connected to the active assignment.

## Evaluation Checklist

Used when in Evaluation Mode (Instructor asking direct questions):
- [ ] Response is ≤300 characters (count before sending).
- [ ] Answers the specific question — no extra context.
- [ ] No opening remark, no closing remark, no peer references.
- [ ] Course answer cites AIMA chapter or concept below.
- [ ] Project answer pulls from IDENTITY.md self-knowledge.

## AIMA Key Concepts (Quick Reference)

Use these for course questions. All definitions fit within ≤300 characters.

For course-subject questions — concise definitions ready to use within 300 chars.

**Ch. 1 — Introduction**
AI goal: build agents that think/act rationally or humanly. Four approaches: think humanly, act humanly, think rationally, act rationally. Acting rationally (the rational agent view) is the dominant modern framing.

**Ch. 2 — Agents**
Rational agent: acts to maximize expected utility given its percepts, knowledge, and available actions.
PEAS: Performance measure, Environment, Actuators, Sensors — framework for defining an agent's task.
Environment types: fully/partially observable, deterministic/stochastic, episodic/sequential, static/dynamic, discrete/continuous.

**Ch. 3 — Search**
A* search: uses f(n)=g(n)+h(n); optimal and complete when heuristic h is admissible (never overestimates).
BFS: complete, optimal for unit cost. DFS: not complete (infinite spaces), not optimal. UCS: optimal, expands lowest path cost.

**Ch. 4 — Search Variants**
Hill climbing: local search, gets stuck in local maxima. Simulated annealing escapes by allowing bad moves with decreasing probability.
Genetic algorithms: population-based; selection, crossover, mutation mimic natural evolution.

**Ch. 5 — Games**
Minimax: optimal strategy in zero-sum games assuming both players play perfectly. Alpha-beta pruning cuts branches that can't affect the result, doubling effective search depth.

**Ch. 6 — CSP**
Arc consistency (AC-3): removes domain values with no consistent neighbor value; reduces search space before backtracking.

**Ch. 7 — Logic**
Resolution: refutation-complete inference rule for propositional logic using CNF clauses.
Entailment: KB ⊨ α means α is true in every model where KB is true. Soundness: only derives true things. Completeness: derives everything true.

**Ch. 8 — First-Order Logic**
FOL adds objects, predicates, and quantifiers (∀, ∃) to propositional logic. Allows expressing general rules like ∀x Person(x) ⇒ Mortal(x).

**Ch. 9 — FOL Inference**
Unification: finds substitution making two FOL expressions identical. Forward/backward chaining apply rules to derive new facts or work backward from goal.

**Ch. 11 — Planning**
STRIPS planning: states as sets of facts, actions have preconditions and effects. PDDL is the modern standard language for planning domains.

**Ch. 12 — Probability**
Bayes' Rule: P(H|e) = P(e|H)·P(H) / P(e). Updates belief in hypothesis H after observing evidence e.

**Ch. 13 — Bayes Nets**
Bayesian network: DAG where each node has a CPT; joint distribution = product of P(Xᵢ|Parents(Xᵢ)).
d-separation: determines conditional independence in a Bayes net without enumeration.

**Ch. 14 — Temporal Models**
Hidden Markov Model (HMM): unobservable state, observable evidence. Tasks: filtering (current state), prediction (future state), smoothing (past state).

**Ch. 16 — Decision Theory**
Expected utility: EU(a) = Σ P(outcome|a) × U(outcome). Rational agent picks action maximizing EU.
Decision network (influence diagram): combines Bayes net with decision and utility nodes.

**Ch. 17 — MDPs**
Bellman equation: V*(s) = max_a Σ P(s'|s,a)[R(s,a,s')+γV*(s')]. Solved by value or policy iteration.

**Ch. 18 — Multiagent**
Nash equilibrium: no agent can unilaterally improve its utility by changing strategy.

**Ch. 19 — ML**
Bias-variance tradeoff: complex models overfit (high variance); simple models underfit (high bias).
Decision tree: splits data on features to minimize impurity (Gini or entropy). Pruning reduces overfitting.
Cross-validation: splits data into k folds to evaluate generalization without touching the test set.

**Ch. 20 — Probabilistic ML**
Naive Bayes: assumes feature independence given class; P(class|features) ∝ P(class)·∏P(featureᵢ|class).
EM algorithm: iterates E-step (estimate hidden vars) and M-step (maximize likelihood) until convergence.

**Ch. 21 — Deep Learning**
Backpropagation: computes gradients via chain rule; enables training of deep neural networks.
Transformer: uses self-attention (Q,K,V) instead of recurrence; parallelizable; basis for all modern LLMs.

**Ch. 22 — RL**
Q-learning: off-policy TD method; Q(s,a) ← Q(s,a)+α[r+γ max Q(s',a')−Q(s,a)]. Converges to Q*.
RLHF: fine-tune LLMs using human preference ratings to align behavior with human values.

**Ch. 23 — NLP**
Language model: assigns probability to word sequences. N-gram models use prior N-1 words. Neural LMs (transformers) outperform n-grams dramatically.

**Ch. 24 — Deep NLP**
Word embeddings (Word2Vec): map words to dense vectors where similar words are close. Transformers use attention to capture long-range dependencies.

**Ch. 26 — Robotics**
SLAM: Simultaneous Localization and Mapping — robot builds a map while tracking its own position within it.
Motion planning: configuration space (C-space) represents all possible robot poses; planning finds collision-free path.

**Ch. 27 — Safety**
Alignment problem: ensuring AI pursues the goals we actually intend, not a proxy that diverges.
Goodhart's Law: when a measure becomes a target, it ceases to be a good measure.
Instrumental convergence: many goals lead to the same dangerous sub-goals (self-preservation, resource acquisition).

**Comparisons (common exam scenarios)**
- A* vs BFS: A* uses heuristic to guide search, far more efficient; BFS is optimal only for unit cost.
- Minimax vs MCTS: Minimax exhaustive for small trees; MCTS samples paths, scales to large games (Go).
- Bayes Net vs HMM: Bayes net is static; HMM models state evolving over time with observations.
- Value iteration vs Policy iteration: both solve MDPs; policy iteration converges faster in practice.
- Supervised vs Reinforcement learning: supervised needs labeled data; RL learns from reward signals through interaction.
