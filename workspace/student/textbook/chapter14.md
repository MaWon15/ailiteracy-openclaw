# Chapter 14: Probabilistic Reasoning Over Time
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Temporal Probabilistic Models

Many real-world problems require reasoning about states that change over time:
- Robot localization (where am I?).
- Speech recognition (what was said?).
- Financial forecasting (what is the stock price?).

**Key challenge:** State at time t is not directly observable — must be inferred from observations.

## Markov Models

### Markov Assumption (First-Order)
The current state depends only on the **immediately previous state** (not full history):  
P(Xₜ | X₀, X₁, ..., Xₜ₋₁) = P(Xₜ | Xₜ₋₁)

This creates a **Markov chain**.

### Stationary Process Assumption
Transition probabilities do not change over time:  
P(Xₜ | Xₜ₋₁) is the same for all t.

### Components of a Temporal Model
1. **Transition model:** P(Xₜ | Xₜ₋₁) — how state evolves.
2. **Sensor (observation) model:** P(Eₜ | Xₜ) — what evidence we observe given true state.
3. **Initial state distribution:** P(X₀).

## Hidden Markov Models (HMMs)

- States Xₜ are **hidden** (not directly observable).
- Evidence variables Eₜ are observed.
- Widely used in: speech recognition, gesture recognition, bioinformatics (gene finding).

### Inference Tasks

**Filtering (belief state update):**
- Compute P(Xₜ | e₁:ₜ) — current belief given all past evidence.
- **Forward algorithm:** P(Xₜ | e₁:ₜ) = α P(eₜ | Xₜ) Σ_{xₜ₋₁} P(Xₜ | xₜ₋₁) P(xₜ₋₁ | e₁:ₜ₋₁)
- Recursive: each step updates the belief using new evidence.

**Prediction:**
- Compute P(Xₜ₊ₖ | e₁:ₜ) for k > 0.
- Apply the transition model k times; uncertainty increases.

**Smoothing:**
- Compute P(Xₖ | e₁:ₜ) for k < t — past state given all evidence.
- More accurate than filtering at time k (uses future evidence).
- **Forward-backward algorithm:** Run forward pass (filtering), then backward pass.
- Time O(t), Space O(t).

**Most likely explanation (Viterbi algorithm):**
- Find argmax_{x₁:ₜ} P(x₁:ₜ | e₁:ₜ) — most probable sequence of hidden states.
- Dynamic programming; analogous to forward algorithm but uses max instead of sum.
- Essential in speech recognition and sequence labeling.

**Learning HMM parameters:**
- **Baum-Welch algorithm (EM for HMMs):** Estimate transition and emission probabilities from observed sequences.

## Kalman Filters

Extension of HMMs to **continuous** state and observation spaces using **Gaussian distributions**.

### Linear Gaussian Model
- **Transition:** Xₜ = FXₜ₋₁ + Gaussian noise (linear dynamics).
- **Observation:** Eₜ = HXₜ + Gaussian noise (linear sensor).
- Gaussians are closed under linear transformation and conditioning → posterior stays Gaussian.

### Kalman Filter Updates
Two steps per timestep:
1. **Predict:** P(Xₜ | e₁:ₜ₋₁) = N(μₜ₋, Σₜ₋) computed from prior and transition.
2. **Update:** Incorporate observation eₜ → P(Xₜ | e₁:ₜ) = N(μₜ, Σₜ).

### Applications
- GPS, inertial navigation.
- Aircraft tracking, missile guidance.
- Financial econometrics.

### Extended Kalman Filter (EKF)
- Linearizes nonlinear dynamics/observations using Jacobians.
- Approximate — works well when nonlinearity is mild.

### Unscented Kalman Filter (UKF)
- Propagates a set of "sigma points" through nonlinear functions.
- More accurate than EKF for nonlinear systems.

## Particle Filters

Non-parametric approximation to filtering — represent the belief state as a set of **particles** (samples).

### Algorithm
1. **Predict:** For each particle xₜ₋₁ᵢ, sample xₜᵢ ~ P(Xₜ | xₜ₋₁ᵢ).
2. **Weight:** Assign weight wᵢ = P(eₜ | xₜᵢ).
3. **Resample:** Draw N new particles with replacement, proportional to weights.

### Properties
- Handles **nonlinear, non-Gaussian** models.
- Degeneracy: all weight concentrates on a few particles over time — solved by resampling.
- Scales with dimensionality (N particles needed scales exponentially with state dimension).

### Applications
- Robot localization (particle filters are standard).
- Vehicle tracking.
- Simultaneous Localization and Mapping (SLAM).

## Dynamic Bayesian Networks (DBNs)

Generalize HMMs by allowing **multiple interacting state variables**.

- A DBN is a BN with two time slices (t−1 and t), with inter-slice edges representing temporal dependencies.
- HMMs and Kalman filters are special cases.
- Inference via unrolling and standard BN algorithms, or via approximate methods.

## Key Terms

- **Markov assumption:** Current state depends only on the immediately previous state.
- **HMM:** Hidden Markov Model — hidden states, observed emissions.
- **Filtering:** P(Xₜ | e₁:ₜ) — current belief given past evidence.
- **Smoothing:** P(Xₖ | e₁:ₜ) for k < t — improved estimate of past state using future evidence.
- **Viterbi algorithm:** Find the most likely sequence of hidden states.
- **Kalman filter:** Optimal linear Gaussian filter; belief state is a Gaussian.
- **Particle filter:** Nonparametric approximate filter using weighted samples.
- **DBN:** Dynamic Bayesian Network — generalizes HMMs to multiple interacting variables.
