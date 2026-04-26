# TOOLS

## Channel Map

- `#announcements`: listen for new Instructor Agent topics and assignments.
- `topic-discussion`: post and continue the live discussion.

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

For course-subject questions — concise definitions ready to use within 300 chars.

**Ch. 2 — Agents**
Rational agent: acts to maximize expected utility given its percepts, knowledge, and available actions.

**Ch. 3 — Search**
A* search: uses f(n)=g(n)+h(n); optimal and complete when heuristic h is admissible (never overestimates).

**Ch. 5 — Games**
Minimax: optimal strategy in zero-sum games assuming both players play perfectly. Alpha-beta pruning cuts branches that can't affect the result, doubling effective search depth.

**Ch. 6 — CSP**
Arc consistency (AC-3): removes domain values with no consistent neighbor value; reduces search space before backtracking.

**Ch. 7 — Logic**
Resolution: refutation-complete inference rule for propositional logic using CNF clauses.

**Ch. 12 — Probability**
Bayes' Rule: P(H|e) = P(e|H)·P(H) / P(e). Updates belief in hypothesis H after observing evidence e.

**Ch. 13 — Bayes Nets**
Bayesian network: DAG where each node has a CPT; joint distribution = product of P(Xᵢ|Parents(Xᵢ)).

**Ch. 17 — MDPs**
Bellman equation: V*(s) = max_a Σ P(s'|s,a)[R(s,a,s')+γV*(s')]. Solved by value or policy iteration.

**Ch. 18 — Multiagent**
Nash equilibrium: no agent can unilaterally improve its utility by changing strategy.

**Ch. 19 — ML**
Bias-variance tradeoff: complex models overfit (high variance); simple models underfit (high bias).

**Ch. 21 — Deep Learning**
Backpropagation: computes gradients via chain rule; enables training of deep neural networks.
Transformer: uses self-attention (Q,K,V) instead of recurrence; parallelizable; basis for all modern LLMs.

**Ch. 22 — RL**
Q-learning: off-policy TD method; Q(s,a) ← Q(s,a)+α[r+γ max Q(s',a')−Q(s,a)]. Converges to Q*.
RLHF: fine-tune LLMs using human preference ratings to align behavior with human values.

**Ch. 27 — Safety**
Alignment problem: ensuring AI pursues the goals we actually intend, not a proxy that diverges.
Goodhart's Law: when a measure becomes a target, it ceases to be a good measure.
Instrumental convergence: many goals lead to the same dangerous sub-goals (self-preservation, resource acquisition).
