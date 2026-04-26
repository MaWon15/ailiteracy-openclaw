# Chapter 9: Inference in First-Order Logic
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Propositional vs. First-Order Inference

Propositional inference is decidable but doesn't scale to rich domains. FOL inference is **semidecidable**: if a sentence is entailed, there is a procedure that will eventually find a proof; if it is not entailed, the procedure may run forever.

## Reducing FOL to Propositional Logic

### Instantiation
- **Universal instantiation (UI):** From ∀v α, derive Subst({v/g}, α) for any ground term g.
  - ∀x King(x) → Evil(x) + King(John) → Evil(John).
- **Existential instantiation (EI):** From ∃v α, introduce a new **Skolem constant** k not in KB: Subst({v/k}, α).
  - ∃x Crown(x) → Crown(C₁) for a new constant C₁.

### Propositionalization
- Apply UI and EI exhaustively; reduce to propositional KB; use propositional inference.
- **Problem:** Infinitely many ground terms possible (Herbrand's theorem guarantees completeness if a proof exists, but enumeration may be infinite).
- **Herbrand's theorem:** If a sentence is unsatisfiable, there exists a finite set of ground clauses that is also unsatisfiable.

## Unification

**Unification:** Finding a substitution θ (a **unifier**) that makes two logical expressions identical.

- UNIFY(Knows(John, x), Knows(John, Jane)) = {x/Jane}
- UNIFY(Knows(John, x), Knows(y, Bill)) = {x/Bill, y/John}
- UNIFY(Knows(John, x), Knows(x, Elizabeth)) = fail (x cannot be both John and Elizabeth)

**Most General Unifier (MGU):** The most general substitution — leaves variables as free as possible.

**Occur check:** Before substituting x with a term t, verify x ∉ t. Omitting this (as many implementations do) can cause unsoundness.

## Lift Inference Rules to FOL

### Generalized Modus Ponens
- Combines unification with Modus Ponens.
- From (p₁ ∧ ... ∧ pₙ → q) and p₁', ..., pₙ' where UNIFY(pᵢ, pᵢ') = θ, derive Subst(θ, q).
- Lifts Modus Ponens to work on first-order sentences with variables.
- **Sound and complete for definite clauses.**

### Forward Chaining (FOL)
- Start from known atomic sentences; apply Generalized Modus Ponens to derive new facts.
- Repeat until query is answered or no new facts can be derived.
- **Sound** and **complete for definite clause** KBs.
- **Datalog:** Forward chaining on ground (variable-free) definite clauses — terminates in polynomial time.

### Backward Chaining (FOL)
- Start with the goal; recursively find rules and subgoals that prove it.
- **Prolog:** Programming language based on FOL backward chaining + depth-first search.
- Prolog uses the **database semantics** (closed-world assumption) and **occurs-check-free unification** (practical but unsound).
- Issue: **infinite loops** possible with recursive rules; depth-first may not terminate.

## Resolution in FOL

### Clausal Form (Conjunctive Normal Form for FOL)
Converting to CNF:
1. Eliminate biconditionals and implications.
2. Move negations inward (De Morgan's laws, quantifier negation).
3. Standardize variables (rename to unique names).
4. **Skolemize:** Replace existential quantifiers with Skolem functions/constants.
5. Drop universal quantifiers.
6. Distribute ∨ over ∧.

### FOL Resolution Rule
- From clause C₁ (containing literal l) and clause C₂ (containing ¬m) with UNIFY(l, m) = θ, derive Subst(θ, C₁ ∪ C₂) minus the resolved literals.
- **Resolution refutation:** Negate the query, add to KB, convert to CNF, apply resolution until deriving the empty clause (⊥).
- **Complete for refutation** (Robinson, 1965).

### Completeness: Herbrand's Theorem & Gödel's Theorem
- **Gödel's Completeness Theorem (1930):** Every valid FOL sentence is provable.
- **Gödel's Incompleteness Theorem (1931):** Any consistent formal system strong enough to express arithmetic contains true statements that cannot be proved within it.
- **Semidecidability:** FOL entailment is semidecidable — provable if true, but the procedure may not halt if false.

## Practical Theorem Provers

- **OTTER / Prover9:** Resolution-based provers.
- **Vampire, E, Zipperposition:** Modern competition-grade FOL provers.
- **Isabelle, Coq, Lean:** Interactive theorem provers for verified mathematics.
- **SAT Modulo Theories (SMT):** Combine SAT solving with domain theories (arithmetic, arrays); used in software verification.

## Key Terms

- **Unification:** Finding a substitution that makes two FOL expressions identical.
- **Most General Unifier (MGU):** The most general (least specific) substitution that unifies two expressions.
- **Skolemization:** Replacing existential variables with new constants/functions to eliminate ∃.
- **Generalized Modus Ponens:** Modus Ponens lifted to FOL using unification.
- **Resolution refutation:** Prove KB ⊨ α by showing KB ∧ ¬α is unsatisfiable.
- **Semidecidability:** FOL is complete but not decidable — the proof procedure may not terminate.
