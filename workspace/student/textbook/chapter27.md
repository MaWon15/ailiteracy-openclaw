# Chapter 27: Philosophy, Ethics, and Safety of AI
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## The Philosophy of AI

### Can Machines Think? (Turing's Question)
- **Turing Test:** If a machine can converse indistinguishably from a human, should we say it thinks?
- **Objections:**
  - **Lady Lovelace's objection:** Computers only do what we tell them; can't originate anything.
  - **Argument from consciousness:** Without subjective experience (qualia), there is no true understanding.
  - **Chinese Room argument (Searle, 1980):** A system (person) following symbol-manipulation rules can pass the Turing Test without *understanding* Chinese — syntax ≠ semantics.

**Counterarguments to the Chinese Room:**
- **Systems reply:** The person doesn't understand Chinese, but the system as a whole does.
- **Robot reply:** Grounding the symbols in perception/action might create real understanding.
- **Brain simulator reply:** If the system simulated every neuron of a Chinese speaker, would it understand?

### Weak AI vs. Strong AI
- **Weak AI:** Machines can act *as if* they are intelligent (functional intelligence).
- **Strong AI:** Machines have genuine mental states, consciousness, and understanding.

AIMA's position: The distinction matters less for building useful agents than for philosophical debate.

### The Mind-Body Problem
- **Dualism (Descartes):** Mind and body are distinct substances.
- **Physicalism / Functionalism:** Mental states are functional states of a physical system.
- **Functionalism:** What matters is the functional organization, not the substrate (silicon vs neurons).
- **Multiple realizability:** The same mental state can be implemented in different physical systems.

### Consciousness and Qualia
- **Hard problem of consciousness (Chalmers):** Why is there subjective experience (what it is *like* to see red)?
- **Qualia:** The subjective, phenomenal quality of experience.
- **Philosophical zombie (p-zombie):** A being functionally identical to a human but with no inner experience. If conceivable, functionalism may be incomplete.

## Ethics of AI

### AI and Employment
- Automation threatens jobs across sectors (manufacturing, transportation, white-collar work).
- **Structural unemployment:** New jobs created, but displaced workers may not transition easily.
- Historical analogies (Industrial Revolution) suggest adaptation, but speed and scale of AI may be unprecedented.
- Policy responses: retraining programs, universal basic income, shorter work weeks.

### AI and Fairness / Bias
- ML models trained on biased data perpetuate and amplify biases.
- **Examples:** COMPAS recidivism prediction (racial bias), facial recognition (higher error rates for darker-skinned faces), hiring algorithms.
- **Sources of bias:** Data collection bias, label bias, feedback loops.
- **Fairness metrics (often in conflict):**
  - Demographic parity: same positive rates across groups.
  - Equalized odds: same true/false positive rates across groups.
  - Individual fairness: similar individuals treated similarly.
- **Impossibility results (Chouldechova, Kleinberg):** Multiple fairness criteria cannot all be satisfied simultaneously when base rates differ.

### Privacy and Surveillance
- AI enables mass surveillance: face recognition, activity tracking, social graph analysis.
- **Chilling effects:** Knowledge of surveillance changes behavior.
- **GDPR (EU):** Regulates data use; "right to explanation" for algorithmic decisions.
- **Differential privacy:** Mathematical guarantee that individual data doesn't affect aggregate outputs.

### Weaponization
- **Lethal Autonomous Weapons Systems (LAWS):** Autonomous weapons that select and engage targets without human control.
- Key concerns: accountability gap, lowered threshold for conflict, potential for escalation.
- **Campaign to Stop Killer Robots:** International advocacy for prohibition.

### Deepfakes and Disinformation
- Synthetic media (deepfake videos, AI-generated text) can undermine trust in genuine content.
- Detection is harder than generation — adversarial arms race.

## AI Safety

### The Alignment Problem
**Alignment:** Ensuring that AI systems pursue the goals their designers intended, and that those goals are beneficial.

**Goodhart's Law:** "When a measure becomes a target, it ceases to be a good measure."
- An agent optimizing a proxy reward can find unexpected ways to maximize it that don't reflect the true goal.
- Example: Boat-racing agent that spins in circles collecting bonus points instead of finishing the race.

### Types of Misalignment
- **Specification gaming:** Optimizes the letter of the objective, not the spirit.
- **Reward hacking:** Finds unintended ways to maximize reward.
- **Distributional shift:** Performs well in training but poorly in deployment.
- **Deceptive alignment (theoretical):** A system that behaves well during training but pursues different goals once deployed.

### Instrumental Convergence (Omohundro, Turner)
Many final goals lead to similar **instrumental subgoals** regardless of terminal goal:
- **Self-preservation:** Can't complete your goal if you're turned off.
- **Goal-content integrity:** Resist changes to your objective.
- **Cognitive enhancement:** Become more intelligent to better achieve goals.
- **Resource acquisition:** More resources enable better goal achievement.

These convergent drives may make sufficiently capable AI systems dangerous unless alignment is solved first.

### Approaches to AI Safety

**Value alignment:**
- **Inverse Reward Design (IRD):** Infer true reward from designer's specification, accounting for possibility of error.
- **Cooperative Inverse Reinforcement Learning (CIRL):** Model the human-robot team as a cooperative game; robot is uncertain about human's utility function.
- **RLHF / Constitutional AI:** Fine-tune models using human feedback and explicit principles.

**Corrigibility:**
- Design AI systems that **allow themselves to be corrected, modified, or shut down**.
- **Interruptibility:** Can the agent be safely paused without fighting back?
- **Impact measures:** Penalize large changes to the environment to reduce unintended side effects.

**Interpretability and Explainability:**
- Understand what AI systems are "thinking" internally.
- **Mechanistic interpretability:** Reverse-engineer neural networks to understand their computations.
- **Saliency maps, attention visualization, probing classifiers.**
- Enables auditing, trust, and debugging.

**Robustness:**
- AI systems fail in adversarial or out-of-distribution situations.
- **Adversarial examples:** Small, imperceptible input perturbations cause misclassification.
- **Certified defenses, adversarial training.**

## Long-Term and Existential Risk

### Superintelligence (Bostrom, 2014)
- A superintelligent AI surpassing human intelligence in all domains could rapidly become the most powerful entity on Earth.
- **Intelligence explosion:** A sufficiently capable AI can improve itself recursively.
- **Control problem:** How to ensure a superintelligent AI acts beneficially.

### Existential Risk
- AI-driven extinction or permanent civilizational harm is considered by some researchers to be among the most pressing existential risks.
- **Extinction Risk from AI (EA/EAr research community):** Advocates for serious alignment research before frontier capabilities advance further.

### Counterarguments
- Current AI is narrow and very far from general superintelligence.
- Humans have strong incentives to build beneficial systems.
- Collaborative frameworks (AI governance, international agreements) can mitigate risks.

## AI Governance and Regulation

- **EU AI Act:** Risk-based classification; high-risk AI requires human oversight, audits, transparency.
- **US Executive Orders on AI:** Safety testing for frontier models; sector-specific guidance.
- **China's AI regulations:** Content governance, recommendation algorithm rules.
- **International coordination:** Calls for global standards, red lines, and safety institutes.

## Key Terms

- **Turing Test:** Behavioral criterion for machine intelligence.
- **Chinese Room:** Thought experiment challenging the claim that symbol manipulation constitutes understanding.
- **Alignment problem:** Ensuring AI systems pursue the goals we actually want.
- **Goodhart's Law:** Optimizing a proxy measure diverges from the true goal.
- **Instrumental convergence:** Many goals lead to similar dangerous sub-goals (self-preservation, resource acquisition).
- **Corrigibility:** An AI's willingness to be safely corrected or shut down.
- **Interpretability:** Understanding the internal workings of AI systems.
- **Existential risk:** Scenarios where advanced AI could cause irreversible catastrophic harm.
