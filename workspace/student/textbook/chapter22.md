# Chapter 22: Reinforcement Learning
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is Reinforcement Learning?

An **RL agent** learns by interacting with an environment — taking actions and observing rewards — without explicit supervision.

**Key distinctions from supervised learning:**
- No labeled "correct action" — only a delayed reward signal.
- Agent must **explore** to discover good actions.
- Actions have **long-term consequences** — credit assignment is hard.

## The RL Setting

Formally an **MDP** (or POMDP) where the transition model and reward function are **unknown**:
- Agent observes state sₜ.
- Agent selects action aₜ.
- Environment transitions to sₜ₊₁ ~ P(s′|sₜ, aₜ).
- Agent receives reward rₜ = R(sₜ, aₜ).
- Goal: Maximize expected discounted return G = Σₜ γᵗ rₜ.

## Passive Reinforcement Learning

The agent follows a **fixed policy** and learns to evaluate it.

### Direct Utility Estimation
- Sample many episodes; estimate V^π(s) = average return from state s.
- Ignores Markov property — slow convergence.

### Temporal Difference (TD) Learning
Update value estimate using adjacent timesteps:  
V(sₜ) ← V(sₜ) + α [rₜ + γ V(sₜ₊₁) − V(sₜ)]

- **TD error (δ):** rₜ + γ V(sₜ₊₁) − V(sₜ) — the "prediction error."
- Bootstraps: updates based on current estimates, not full rollout.
- More efficient than Monte Carlo; can learn online.

### TD(λ) and Eligibility Traces
- **λ = 0:** TD(0) — one-step look-ahead.
- **λ = 1:** Monte Carlo — full episode return.
- **λ ∈ (0,1):** Intermediate — exponentially weighted multi-step returns.
- **Eligibility trace e(s):** Accumulates recency of visits; propagates credit backward.

## Active Reinforcement Learning (Q-Learning and Policy Learning)

The agent must also **choose actions** to maximize reward — the exploration-exploitation tradeoff.

### Q-Learning (Off-Policy TD)
Learn the **action-value function** Q(s, a):  
Q(sₜ, aₜ) ← Q(sₜ, aₜ) + α [rₜ + γ max_{a′} Q(sₜ₊₁, a′) − Q(sₜ, aₜ)]

- **Off-policy:** Learns optimal Q regardless of the behavior policy used.
- Converges to Q* with probability 1 under mild conditions (all (s,a) visited infinitely often).

### SARSA (On-Policy TD)
Q(sₜ, aₜ) ← Q(sₜ, aₜ) + α [rₜ + γ Q(sₜ₊₁, aₜ₊₁) − Q(sₜ, aₜ)]

- **On-policy:** Learns Q for the actual policy being followed.
- Safer in practice when exploration is dangerous.

## Exploration vs. Exploitation

- **ε-greedy:** With probability ε take a random action; otherwise take the best known action.
- **Softmax / Boltzmann exploration:** Select action with probability proportional to e^(Q(a)/T).
- **Optimism in the face of uncertainty:** Initialize Q values optimistically; agent naturally explores under-visited states.
- **UCB (Upper Confidence Bound):** Select action with highest Q(a) + c √(ln t / n(a)).
- **Thompson sampling:** Bayesian exploration — sample from posterior over Q values.

## Generalization in RL: Function Approximation

Tabular Q-learning fails when state spaces are continuous or very large.

### Linear Function Approximation
Q(s, a; θ) = θᵀ φ(s, a) where φ(s, a) is a feature vector.

Updates: θ ← θ + α δ φ(s, a) where δ is the TD error.

### Deep Reinforcement Learning

**Deep Q-Network (DQN) — Mnih et al., 2013:**
- Represent Q(s, a; θ) with a deep neural network.
- **Experience replay:** Store transitions (s, a, r, s′) in a replay buffer; sample random mini-batches. Breaks correlations between consecutive samples.
- **Target network:** Separate (frozen) network for computing TD targets; updated periodically. Stabilizes training.
- Achieved superhuman performance on 49 Atari games from raw pixels.

## Policy Gradient Methods

Instead of learning a value function, directly optimize the policy π_θ.

**Policy gradient theorem:**  
∇_θ J(θ) = E_π [∇_θ log π_θ(a|s) × Q^π(s, a)]

### REINFORCE Algorithm
- Sample trajectory; compute return G_t; update θ ← θ + α G_t ∇_θ log π_θ(aₜ|sₜ).
- **High variance** — reduce with baselines (subtract V(s) from return: advantage A = G_t − V(sₜ)).

### Actor-Critic Methods
- **Actor:** Policy π_θ selects actions.
- **Critic:** Value function V_φ estimates returns.
- Critic reduces variance of policy gradient; actor uses these estimates to improve.
- **A3C (Asynchronous Advantage Actor-Critic):** Multiple parallel agents.
- **PPO (Proximal Policy Optimization):** Clips policy updates to avoid large steps — stable and widely used.
- **SAC (Soft Actor-Critic):** Off-policy actor-critic with entropy regularization for exploration.

## Advanced Topics

### Model-Based RL
- Learn a model of the environment P(s′|s,a) and R(s,a).
- Plan using the learned model (Dyna architecture: real + simulated experience).
- **AlphaZero:** Model-based RL + MCTS; learns to play chess, Go, shogi from self-play.

### Multi-Task and Meta-RL
- **Multi-task RL:** Train a policy to solve multiple tasks simultaneously.
- **Meta-RL:** "Learning to learn" — quickly adapt to new tasks with few samples (MAML).

### Reward Shaping
- Provide additional intermediate rewards to help the agent learn.
- Must be done carefully to avoid changing the optimal policy.

### Inverse Reinforcement Learning (IRL)
- Given demonstrations from an expert, infer the reward function.
- Applications: Imitation learning, RLHF (Reinforcement Learning from Human Feedback).

### RLHF (Reinforcement Learning from Human Feedback)
- Use human preference ratings (rather than a fixed reward) to train a reward model.
- Fine-tune LLMs to follow instructions, be helpful and harmless.
- Core technique behind ChatGPT and Claude alignment.

## Key Terms

- **Q-learning:** Off-policy TD method for learning the optimal action-value function.
- **SARSA:** On-policy TD method.
- **Deep Q-Network (DQN):** Q-learning with deep neural network + experience replay + target network.
- **Policy gradient:** Directly optimize policy parameters; REINFORCE is the basic algorithm.
- **Actor-Critic:** Combines policy gradient (actor) with value estimation (critic).
- **PPO:** Proximal Policy Optimization — stable, widely-used policy gradient method.
- **Exploration-exploitation:** Tradeoff between trying new actions and using known good ones.
- **RLHF:** Reinforcement Learning from Human Feedback — used to align LLMs.
