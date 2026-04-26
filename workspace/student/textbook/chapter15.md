# Chapter 15: Probabilistic Programming
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is Probabilistic Programming?

**Probabilistic programming** combines the expressiveness of general-purpose programming languages with probabilistic inference.

- A **probabilistic program** defines a probability distribution over program executions.
- Rather than writing a model as a Bayesian network (a fixed graph), a probabilistic program can define distributions over structures, use arbitrary computation, and handle open-universe models.

## Relational Probability Models (RPMs)

Standard Bayesian networks use a fixed set of variables. Real-world domains have **objects** and **relations** (like FOL), and the number of objects may vary.

### Probabilistic Relational Models (PRMs)
- Combine first-order logic structure with probabilistic dependencies.
- Template for Bayesian networks over typed objects and their relations.
- **Variable nodes** (with CPTs) parameterized by object types and role-filler objects.
- Generate a ground BN by instantiating templates for specific domain objects.

### Example: Academic World
- Objects: Students, Professors, Papers, Courses.
- Relations: Advises(Prof, Student), AuthorOf(Student, Paper).
- Random variables: Student.GPA, Paper.Quality — dependencies via relational structure.

## Open-Universe Probability Models

Standard models require a fixed set of objects (closed-world). **Open-universe** models allow the number and identity of objects to be uncertain.

**BLOG (Bayesian Logic):**
- Extends Bayesian reasoning to unknown numbers of objects.
- Declare number models (how many objects exist) and CPTs.
- Example: "How many aircraft are there? Each aircraft has a type and location. Radar returns are noisy observations."
- Handles **identity uncertainty**: are two detections the same object?

## Probabilistic Programming Languages

### Church
- Based on Scheme/Lisp; uses `sample` and `condition` constructs.
- Any computable distribution can be defined.
- Inference via MCMC over program traces.

### Venture
- Mutable state; supports sequential models.

### Pyro (PyTorch)
- Deep probabilistic programming language.
- Integrates neural networks with probabilistic models.
- Inference via variational methods and MCMC.

### Stan
- Probabilistic programming for statistical modeling.
- Inference via Hamiltonian Monte Carlo (HMC) / NUTS.
- Widely used in statistics and social science.

### Probabilistic Soft Logic (PSL)
- Continuous truth values; soft constraints.
- Efficient inference for large-scale relational models.

## Inference in Probabilistic Programs

The key operation: given observations (evidence), compute the posterior distribution over unknowns.

### Rejection Sampling (on traces)
- Sample random choices; reject execution traces inconsistent with evidence.
- Simple but inefficient for low-probability evidence.

### Importance Sampling / Likelihood Weighting
- Weight traces by the probability of evidence.

### MCMC over Traces (Metropolis-Hastings)
- Propose changes to random choices; accept/reject based on likelihood ratio.
- **Trace MCMC:** Standard approach in Church-like languages.

### Variational Inference
- Approximate posterior with a tractable family of distributions; minimize KL divergence.
- Used in Pyro, Edward, TensorFlow Probability.
- Scales to large datasets (Stochastic Variational Inference with minibatches).

### Hamiltonian Monte Carlo (HMC)
- Uses gradient information to make more efficient MCMC proposals.
- **NUTS (No U-Turn Sampler):** Adaptive HMC; used in Stan and PyMC3.
- Much faster mixing than random-walk Metropolis for continuous variables.

## Temporal and Relational Models

- DBNs and HMMs can be expressed as probabilistic programs.
- **Particle MCMC:** Combines particle filters and MCMC for sequential models.
- **Sequential Monte Carlo (SMC):** Particle filtering as a special case of sequential importance resampling.

## Applications of Probabilistic Programming

- **Medical diagnosis:** Flexible symptom-disease models with uncertain evidence.
- **Computer vision:** Generative models of scenes; invert them to infer scene structure.
- **Natural language processing:** Probabilistic grammars; coreference resolution.
- **Robotics:** Sensor fusion, localization, SLAM.
- **Cognitive science:** Bayesian models of cognition (probabilistic programs as theories of mind).

## Key Terms

- **Probabilistic programming:** Programming languages that define probability distributions over computations.
- **Relational probability model:** Template-based BN over typed relational domains.
- **Open-universe model:** Allows uncertain numbers and identities of objects.
- **BLOG:** Bayesian Logic — probabilistic program language for open-universe models.
- **Variational inference:** Approximate inference by optimizing a tractable approximation to the posterior.
- **HMC / NUTS:** Gradient-based MCMC methods for efficient sampling from continuous distributions.
- **Trace MCMC:** MCMC over execution traces of probabilistic programs.
