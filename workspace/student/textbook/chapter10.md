# Chapter 10: Knowledge Representation
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## The Knowledge Representation Problem

Intelligent agents need to represent general knowledge about the world — not just specific facts. This requires:
- **Ontological engineering:** Designing a vocabulary (what concepts exist and how they relate).
- **Epistemological engineering:** Determining what can be known and how.

The **upper ontology** (or top-level ontology) defines the most general categories applicable across all domains.

## Categories and Objects

### Objects and Categories
- Objects are grouped into **categories** (sets, types, classes).
- **Subclass relation (SubclassOf):** Inherits properties.
- **Instance relation (InstanceOf):** An individual belongs to a category.
- **Inheritance:** Properties of a category propagate to its instances.

### Reification
- Treating abstract things (actions, events, propositions) as objects.
- Allows making statements *about* sentences (meta-representation).

### Natural Kinds
- Real-world categories (gold, water) defined by intrinsic properties, not just enumeration.
- **Necessary and sufficient conditions** often cannot be stated precisely — a core challenge of knowledge representation.

## Measures and Units

- **Measures:** Properties with values and units (length, mass, temperature).
- **Dimensions:** Qualitative or quantitative scales.
- Representation: Measure(2.3, Inches) or via dimensional analysis.

## Time, Events, and Actions

### Event Calculus
- Represent events and their effects on fluents (time-varying properties).
- Key predicates: **Happens(e, t)** — event e occurs at time t; **HoldsAt(f, t)** — fluent f is true at t; **Initiates(e, f, t)** — event starts fluent; **Terminates(e, f, t)** — event ends fluent.

### Situation Calculus
- A classical FOL approach to reasoning about change.
- **Situations (S₀, S₁, ...):** Snapshots of world state.
- **Fluents:** Properties that may change. e.g., Holds(Broken(Vase), s).
- **Actions:** Result(a, s) = s′ — the situation after performing action a in situation s.
- **Frame problem:** How to represent what *doesn't* change after an action? Solved with **successor state axioms** and the **closed world assumption for change**.

## Mental Objects and Modal Logic

- **Beliefs, desires, intentions:** Propositional attitudes that agents hold toward propositions.
- **Modal logic:** Extends FOL with operators:
  - **□ (necessarily):** True in all possible worlds.
  - **◇ (possibly):** True in some possible world.
  - **B(agent, p):** Agent believes proposition p.
  - **K(agent, p):** Agent knows p.
- **Possible worlds semantics (Kripke structures):** Modal operators evaluated across a set of accessible worlds.

## Reasoning Systems for Categories

### Semantic Networks
- Graph-based knowledge representation.
- Nodes = objects or categories; edges = relations (isa, haspart, etc.).
- **Inheritance hierarchy:** Enables property inheritance.
- **Ambiguity:** Competing inference chains; no formal semantics by default.

### Description Logics (DLs)
- Formal language for defining ontologies.
- Concepts (classes), roles (properties), individuals.
- **TBox:** Terminological knowledge (concept definitions, subsumption axioms).
- **ABox:** Assertional knowledge (individual facts).
- Supported reasoning: **subsumption checking**, **instance checking**, **consistency checking**.
- Basis for **OWL (Web Ontology Language)** — the standard for knowledge graphs and the Semantic Web.

### Frames
- Structured knowledge representation: a **frame** has slots (attributes) with values.
- Precursor to object-oriented programming and modern ontology systems.

## Non-Monotonic Reasoning

**Monotonic logic:** Adding new sentences can only add new conclusions — nothing is retracted.

**Non-monotonic reasoning:** Conclusions can be retracted as new information arrives.

### Default Reasoning
- **Default logic (Reiter):** Default rules fire unless blocked by contrary information.
  - Default: "Birds can fly" — overridden by "Tweety is a penguin."
- **Closed-world assumption (CWA):** What is not known to be true is assumed false. Common in databases (Prolog), not always appropriate.
- **Open-world assumption (OWA):** Absence of information doesn't imply falsity. Used in OWL/description logics.

### Truth Maintenance Systems (TMS)
- Track justifications for beliefs; retract beliefs when their justifications are invalidated.
- **JTMS:** Justification-based TMS — maintains dependency graph.
- **ATMS:** Assumption-based TMS — tracks multiple consistent assumption sets simultaneously.

## Internet Shopping World (Case Study)

- Demonstrates ontology design for e-commerce: Products, Offers, Stores, Prices.
- Challenges: ambiguous product names, varying units, missing data, conflicting offers.
- Illustrates practical challenges in real-world knowledge engineering.

## Key Terms

- **Ontological engineering:** Designing the vocabulary and structure for a knowledge base.
- **Semantic network:** Graph-based KB with nodes (objects) and edges (relations).
- **Description logic:** Formal language for ontologies with decidable reasoning.
- **OWL:** Web Ontology Language — standard knowledge representation for the Semantic Web.
- **Default reasoning:** Conclusions hold by default unless contradicted.
- **Frame problem:** How to efficiently represent what stays the same after an action.
- **Non-monotonic reasoning:** Ability to retract conclusions when new evidence arrives.
