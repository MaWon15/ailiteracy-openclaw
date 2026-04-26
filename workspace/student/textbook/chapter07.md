# Chapter 7: Logical Agents
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Knowledge-Based Agents

A **knowledge-based agent** uses a **knowledge base (KB)** — a set of sentences in a formal language — to represent the world and reason about it.

Two core operations:
- **TELL:** Add new sentences to the KB (perception, facts).
- **ASK:** Query the KB for consequences (reasoning, action selection).

**Knowledge level:** What the agent knows (declarative).
**Implementation level:** How it is stored and processed (procedural).

**Declarative approach:** Knowledge is explicit and inspectable — separates *what* is known from *how* to use it.

## Logic Fundamentals

- **Syntax:** Rules for forming valid sentences.
- **Semantics:** Rules for interpreting sentences — assigns truth values.
- **Model:** An assignment of truth values to all propositions (a possible world).
- **Entailment (⊨):** KB ⊨ α means α is true in every model in which KB is true.
- **Inference (⊢):** KB ⊢ α means α can be derived from KB using an inference procedure.

**Soundness (truth-preserving):** An inference algorithm is sound if KB ⊢ α implies KB ⊨ α.
**Completeness:** An inference algorithm is complete if KB ⊨ α implies KB ⊢ α.

## Propositional Logic

**Atoms:** Propositional symbols (P, Q, R...) — true or false.

**Connectives:**
| Symbol | Name | Meaning |
|---|---|---|
| ¬ | Negation | NOT |
| ∧ | Conjunction | AND |
| ∨ | Disjunction | OR |
| → | Implication | IF...THEN |
| ↔ | Biconditional | IF AND ONLY IF |

**Truth table** defines semantics for all connectives.

**Important equivalences:**
- Contrapositive: (α → β) ≡ (¬β → ¬α)
- De Morgan: ¬(α ∧ β) ≡ (¬α ∨ ¬β)
- Implication elimination: (α → β) ≡ (¬α ∨ β)

## Inference in Propositional Logic

### Model Checking (Truth Table Enumeration)
- Enumerate all 2^n models; check whether KB ⊨ α in all models where KB is true.
- **Complete** for propositional logic.
- **Exponential:** O(2^n) time — impractical for large KBs.

### Modus Ponens
- From (α → β) and α, derive β.
- Sound and fast; not complete on its own.

### Resolution
- **Resolution rule:** From (l₁ ∨ ... ∨ lₖ) and (m₁ ∨ ... ∨ mₙ) where lᵢ = ¬mⱼ, derive (l₁ ∨ ... ∨ lᵢ₋₁ ∨ lᵢ₊₁ ∨ ... ∨ lₖ ∨ m₁ ∨ ... ∨ mⱼ₋₁ ∨ mⱼ₊₁ ∨ ... ∨ mₙ).
- **Resolution refutation:** To prove KB ⊨ α, show KB ∧ ¬α is unsatisfiable.
- Requires **conjunctive normal form (CNF):** Conjunction of disjunctions (clauses).
- **Complete for refutation.**

### Forward and Backward Chaining (Horn Clauses)
- **Horn clause:** At most one positive literal (A ∧ B → C or just A).
- **Forward chaining:** From known facts, apply Modus Ponens repeatedly to derive new facts. Data-driven.
- **Backward chaining:** Work backward from goal; prove subgoals. Goal-driven.
- Both are **linear time** and **sound and complete for Horn clause KBs**.

## The Wumpus World

A classic test environment for logical agents:
- 4×4 grid, agent starts at [1,1].
- **Percepts:** Stench (adjacent wumpus), Breeze (adjacent pit), Glitter (gold), Bump (wall), Scream (wumpus killed).
- **Actions:** Move forward, turn left/right, grab, shoot, climb.
- **Goal:** Find gold, return to start.

Agent uses propositional logic to:
- Infer safe squares (no wumpus, no pit).
- Infer wumpus location to shoot it.
- Navigate and retrieve gold.

Demonstrates how logical inference enables safe navigation under uncertainty — and its limitations (propositional logic requires many sentences for a 4×4 grid, and cannot handle time or identity efficiently).

## Propositional Satisfiability (SAT)

**SAT problem:** Is there an assignment of truth values that satisfies a given CNF formula?

- **NP-complete** in general.
- **DPLL algorithm:** Systematic backtracking with:
  - **Unit propagation:** If a clause has one unset literal, it must be true.
  - **Pure symbol heuristic:** A symbol appearing with only one polarity can be assigned that value.
  - Recursive splitting on unset variables.
- **WALKSAT:** Local search for SAT — flip unsatisfied clause variables randomly. Very effective in practice.
- **SAT solvers (CDCL):** Conflict-Driven Clause Learning — state-of-the-art. Used in hardware verification, planning.

## Key Terms

- **Knowledge base (KB):** Set of sentences representing what the agent knows.
- **Entailment (⊨):** Logical consequence — true in all models of the KB.
- **Modus Ponens:** Inference rule: from α→β and α, derive β.
- **Resolution:** Complete refutation-based inference rule using CNF.
- **Horn clause:** Clause with at most one positive literal; enables efficient inference.
- **Forward/Backward chaining:** Linear-time complete inference for Horn clause KBs.
- **DPLL:** Systematic SAT algorithm with unit propagation and pure symbol heuristics.
