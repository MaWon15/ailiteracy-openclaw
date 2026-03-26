# Week 3 Lecture Notes: Knowledge Representation and Logical Reasoning

## Knowledge Representation

### What is Knowledge?
- **Facts**: True statements about the world
- **Rules**: Relationships and inferences
- **Concepts**: Categories and classifications
- **Procedures**: How to perform tasks

### Representation Challenges
- **Expressiveness**: Can the representation capture what we need?
- **Efficiency**: Can we compute with it efficiently?
- **Comprehensibility**: Can humans understand and modify it?
- **Adequacy**: Does it match our reasoning needs?

## Propositional Logic

### Syntax
- **Atomic propositions**: P, Q, R (basic statements)
- **Connectives**: ¬ (not), ∧ (and), ∨ (or), → (implies), ↔ (iff)
- **Complex formulas**: Built from atoms and connectives

### Semantics
- **Truth values**: True (T) or False (F)
- **Truth tables**: Define meaning of connectives
- **Models**: Assignments of truth values to atoms

### Example
- P: "It is raining"
- Q: "I will take an umbrella"
- P → Q: "If it is raining, I will take an umbrella"

## First-Order Logic (FOL)

### Components
- **Constants**: Specific objects (John, Mary, 42)
- **Variables**: Placeholders (x, y, z)
- **Predicates**: Relations (Loves, Parent, LargerThan)
- **Functions**: Mappings (FatherOf, Plus, CapitalOf)
- **Quantifiers**: ∀ (forall), ∃ (exists)

### Example Sentences
- ∀x Person(x) → ∃y Loves(y, x)  ("Everyone has someone who loves them")
- ∃x ∀y ¬LargerThan(y, x)  ("There is a largest number")
- ∀x ∀y (Parent(x, y) → ¬Parent(y, x))  ("No one is their own parent")

### Expressiveness vs Propositional Logic
- **Objects and relations**: Can talk about specific individuals
- **Quantification**: Can make general statements
- **Functions**: Can represent computations

## Knowledge Base Systems

### Components
- **Knowledge Base (KB)**: Set of logical sentences
- **Inference Engine**: Derives new knowledge from existing knowledge
- **Query System**: Answers questions about the knowledge

### Inference Methods
- **Forward Chaining**: Start with facts, apply rules to derive conclusions
- **Backward Chaining**: Start with query, find rules that could prove it
- **Resolution**: General method for theorem proving

### Example: Family Relationships
```
KB:
Parent(John, Mary)
Parent(Mary, Bob)
∀x ∀y ∀z (Parent(x,y) ∧ Parent(y,z) → Grandparent(x,z))

Query: Grandparent(John, Bob)?
Backward chaining finds the rule and verifies premises.
```

## Reasoning with Uncertainty

### Why Uncertainty?
- **Incomplete information**: Don't know all facts
- **Inaccurate information**: Facts may be wrong
- **Ambiguous information**: Facts may have multiple interpretations
- **Default reasoning**: What normally happens

### Probability Theory
- **Prior probabilities**: Initial beliefs
- **Conditional probabilities**: P(A|B) = probability of A given B
- **Bayes' Rule**: P(H|E) = P(E|H) * P(H) / P(E)

### Example: Medical Diagnosis
- **Symptoms**: Fever, cough, fatigue
- **Diseases**: Flu, cold, pneumonia
- **Probabilities**: P(Disease|Symptoms)

## Ontologies and Semantic Networks

### Semantic Networks
- **Nodes**: Concepts or objects
- **Edges**: Relationships between concepts
- **Inheritance**: IS-A relationships
- **Properties**: HAS relationships

### Example Network
```
Animal
├── Mammal
│   ├── Dog
│   │   ├── Labrador
│   │   └── Poodle
│   └── Cat
└── Bird
    ├── Eagle
    └── Sparrow
```

### Ontologies
- **Formal specifications**: Precise definitions of concepts
- **Relationships**: Defined relationships between concepts
- **Constraints**: Rules about how concepts can be combined
- **Inference**: Automatic reasoning about relationships

## Discussion Questions

1. What are the trade-offs between different knowledge representation schemes?
2. How do you choose between propositional and first-order logic?
3. What are the challenges of representing uncertainty?
4. How can ontologies help with knowledge sharing?

## Key Takeaways

- Knowledge representation is fundamental to AI reasoning
- Different representations suit different problems
- Logic provides formal foundations for knowledge and reasoning
- Uncertainty is common and must be handled appropriately
- Ontologies enable knowledge sharing and reuse

## Practical Applications

- **Expert systems**: Medical diagnosis, troubleshooting
- **Semantic web**: Machine-readable web content
- **Natural language understanding**: Parsing and interpretation
- **Robotics**: Representing the world for planning