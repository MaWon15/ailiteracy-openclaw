# Chapter 8: First-Order Logic
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Why First-Order Logic?

Propositional logic treats the world as made up of atomic facts. **First-order logic (FOL)** (also: predicate logic, first-order predicate calculus) allows representation of:
- **Objects:** Things in the world (people, places, numbers).
- **Properties:** Attributes of objects (red, tall, prime).
- **Relations:** Relationships between objects (Brother(x, y), Loves(x, y)).
- **Functions:** Maps objects to objects (LeftLeg(x), Father(x)).

FOL subsumes propositional logic and is **far more expressive** while remaining decidable for some fragments.

## Syntax of First-Order Logic

### Terms (denote objects)
- **Constants:** John, 42, Paris — name specific objects.
- **Variables:** x, y, z — range over objects.
- **Functions:** Father(John), LeftLeg(x) — map objects to objects.

### Atomic Sentences (facts about objects)
- Predicate applied to terms: Loves(John, Mary), Prime(7).
- Equality: x = y.

### Complex Sentences (using connectives)
- Same logical connectives as propositional logic: ¬, ∧, ∨, →, ↔.

### Quantifiers
- **Universal quantifier (∀):** ∀x P(x) — "For all x, P(x) holds."
  - Typically used with implication: ∀x (King(x) ∧ Greedy(x) → Evil(x))
- **Existential quantifier (∃):** ∃x P(x) — "There exists an x such that P(x) holds."
  - Typically used with conjunction: ∃x (Crown(x) ∧ OnHead(x, John))

### Quantifier Duality (De Morgan for quantifiers)
- ∀x P(x) ≡ ¬∃x ¬P(x)
- ∃x P(x) ≡ ¬∀x ¬P(x)
- ¬∀x P(x) ≡ ∃x ¬P(x)
- ¬∃x P(x) ≡ ∀x ¬P(x)

### Nested Quantifiers
- Order matters: ∀x ∃y Loves(x, y) ≠ ∃y ∀x Loves(x, y).
- The first: "Everyone loves someone." The second: "There is someone loved by everyone."

## Semantics of First-Order Logic

A **model** in FOL includes:
- A non-empty **domain** of objects.
- An **interpretation** that maps constants to objects, predicates to relations, functions to function mappings.

A sentence is **true** in a model relative to a **variable assignment**.

**Entailment:** KB ⊨ α if α is true in every model that satisfies KB — same definition as propositional logic, but models are now richer.

## Knowledge Engineering in FOL

**Knowledge engineering process:**
1. Identify the task.
2. Assemble relevant knowledge.
3. Decide on vocabulary (predicates, functions, constants).
4. Encode general knowledge about the domain.
5. Encode the specific problem instance.
6. Pose queries and use the inference procedure.
7. Debug and refine the knowledge base.

## Example Domains

### The Kinship Domain
- Predicates: Parent, Child, Sibling, Brother, Sister, Grandparent, Ancestor, Married...
- Example: ∀x ∀y Parent(x, y) ↔ Child(y, x)
- Example: ∀x ∀y Sibling(x, y) ↔ (x ≠ y ∧ ∃p Parent(p, x) ∧ Parent(p, y))

### The Numbers Domain
- Uses standard predicates: NatNum, Integer, >, =, + ...
- Peano axioms define natural numbers in FOL.

### The Set Domain
- Member, Subset, Intersection, Union, Complement...
- ∀x ∀s Member(x, s) ↔ ... (recursive definition)

### The Lists Domain
- Nil, Cons, First, Rest, Append...

### The Wumpus World
- Location-specific predicates; avoids propositional explosion.
- ∀x ∀y Adjacent(x, y) ∧ Breezy(x) → ∃p Pit(p) ∧ Adjacent(p, x)

## Equality

- **Equal(x, y)** or **x = y** — the two terms denote the same object.
- Used to state uniqueness: ∃x Crown(x) ∧ ∀y Crown(y) → y = x (at most one crown).

## Key Terms

- **First-order logic (FOL):** Logic with objects, relations, functions, and quantifiers.
- **Predicate:** A function from objects to truth values representing properties or relations.
- **Universal quantifier (∀):** "For all" — statement holds for every object in the domain.
- **Existential quantifier (∃):** "There exists" — at least one object satisfies the condition.
- **Term:** An expression denoting an object (constant, variable, or function application).
- **Model (FOL):** A domain of objects plus an interpretation of predicates and functions.
- **Closed-world assumption:** Anything not stated in the KB is assumed false.
