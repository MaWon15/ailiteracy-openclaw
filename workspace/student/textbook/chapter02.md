# Chapter 2: Intelligent Agents
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## Agents and Environments

- **Agent:** Anything that perceives its environment through **sensors** and acts upon it through **actuators**.
- **Percept:** The agent's perceptual input at any given instant.
- **Percept sequence:** The complete history of everything an agent has perceived.
- **Agent function:** Maps any percept sequence to an action — a mathematical description of agent behavior.
- **Agent program:** The concrete implementation of the agent function running on physical hardware.

## Rationality

A **rational agent** selects actions that maximize its expected performance measure, given:
1. The performance measure that defines success.
2. The agent's prior knowledge of the environment.
3. The actions the agent can perform.
4. The agent's percept sequence to date.

**Rationality ≠ omniscience.** A rational agent maximizes *expected* performance; it cannot know actual outcomes in advance.

**Rationality ≠ clairvoyance.** Agents must also gather information (exploration) to reduce uncertainty.

**Rationality requires learning.** Agents should update behavior based on experience.

## PEAS Framework

To design a rational agent, specify the **Task Environment** using PEAS:
- **P**erformance measure — how success is evaluated.
- **E**nvironment — the external world the agent interacts with.
- **A**ctuators — the agent's available actions.
- **S**ensors — how the agent perceives the world.

**Example — Self-driving taxi:**
- Performance: Safety, speed, legality, passenger comfort, profit.
- Environment: Roads, traffic, pedestrians, customers, weather.
- Actuators: Steering, accelerator, brake, horn, display.
- Sensors: Cameras, LIDAR, GPS, odometer, microphone.

## Properties of Task Environments

| Property | Description |
|---|---|
| **Fully vs. partially observable** | Can the agent sense the complete state of the environment? |
| **Single-agent vs. multiagent** | One agent or multiple competing/cooperating agents? |
| **Deterministic vs. nondeterministic** | Is the next state fully determined by current state and action? |
| **Episodic vs. sequential** | Does the current decision affect future episodes? |
| **Static vs. dynamic** | Does the environment change while the agent deliberates? |
| **Discrete vs. continuous** | Are states, time, and actions finite or continuous? |
| **Known vs. unknown** | Does the agent know the environment's laws of physics? |

Most real-world problems are: partially observable, multiagent, nondeterministic, sequential, dynamic, continuous, and known.

## Agent Types (in increasing order of capability)

### 1. Simple Reflex Agents
- Select actions based only on the current percept.
- Use condition–action rules (if *condition* then *action*).
- Fail in partially observable environments — no memory of history.

### 2. Model-Based Reflex Agents
- Maintain an **internal state** to track aspects of the world not currently visible.
- Requires a **transition model** (how the world evolves) and a **sensor model** (what percepts look like).
- Can handle partial observability.

### 3. Goal-Based Agents
- Have **goals** describing desirable states.
- Choose actions that lead to goal states — involves search and planning.
- More flexible than reflex agents: goals can change without rewriting rules.

### 4. Utility-Based Agents
- Use a **utility function** mapping states to a real number (degree of happiness).
- Choose actions that maximize expected utility.
- Handle conflicting goals and uncertain outcomes via probability theory.

### 5. Learning Agents
- Improve performance over time through experience.
- Components:
  - **Learning element:** Makes improvements.
  - **Performance element:** Selects actions (the agent described above).
  - **Critic:** Evaluates performance against a fixed standard.
  - **Problem generator:** Suggests exploratory actions to gain new experiences.

## Representation of Agent States

- **Atomic:** Each state is indivisible (used in search, game-playing, MDPs).
- **Factored:** Each state has attribute-value pairs (used in constraint satisfaction, planning, Bayesian networks, ML).
- **Structured:** States involve objects, relations between objects (used in first-order logic, knowledge bases).

## Key Terms

- **Agent:** Perceives environment, acts upon it.
- **Rational agent:** Maximizes expected performance.
- **PEAS:** Framework for specifying task environments.
- **Utility function:** Maps world states to a numeric measure of preference.
- **Learning agent:** Improves its own performance element through experience.
