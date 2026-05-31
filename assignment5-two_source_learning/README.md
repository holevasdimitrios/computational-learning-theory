# Assignment 5: Two-Source PAC Learning Equivalence Bounds

## Problem Formulation
This assignment explores a fundamental variation of the Probably Approximately Correct ($PAC$) learning paradigm. Instead of pulling independent samples from a single, unified distribution $\mathcal{D}$ over the instance space $\mathcal{X}$, the learner interacts with two isolated, label-conditional oracles:
* **Positive Source ($\mathcal{D}^+$):** Generates samples strictly drawn from the positive support domain $\mathcal{X}^+ = \{x \in \mathcal{X} : f(x) = +1\}$.
* **Negative Source ($\mathcal{D}^-$):** Generates samples strictly drawn from the negative support domain $\mathcal{X}^- = \{x \in \mathcal{X} : f(x) = -1\}$.

The objective is to establish an information-theoretic reduction proving that a hypothesis class $\mathcal{H}$ is standard $PAC$ learnable if and only if it is learnable under the conditional two-source sampling framework.

---

## Theoretical Framework & Mathematical Proof Preview

### Part (a): Standard PAC Learning Implies Two-Source Learnability
Assume $\mathcal{H}$ is learnable in the standard $PAC$ model. We define the conditional probabilities over any subset $\mathcal{A}$:
$$\mathcal{D}^+(\mathcal{A}) = \frac{\mathcal{D}(\mathcal{A})}{\mathcal{D}(\mathcal{X}^+)} \quad \text{and} \quad \mathcal{D}^-(\mathcal{A}) = \frac{\mathcal{D}(\mathcal{A})}{\mathcal{D}(\mathcal{X}^-)}$$
Letting $p^+ = \mathcal{D}(\mathcal{X}^+)$ and $p^- = \mathcal{D}(\mathcal{X}^-) = 1 - p^+$, we can flawlessly reconstruct the latent global distribution $\mathcal{D}$ by running a randomized hybrid simulator:
1. Flip a biased coin with success probability $p^+$.
2. If heads, draw an instance $x$ from the conditional oracle $\mathcal{D}^+$.
3. If tails, draw an instance $x$ from the conditional oracle $\mathcal{D}^-$.

The synthesized distribution satisfies:
$$\Pr[x \in \mathcal{A}] = p^+ \cdot \mathcal{D}^+(\mathcal{A}) + p^- \cdot \mathcal{D}^-(\mathcal{A}) = \mathcal{D}(\mathcal{A})$$
Feeding these reconstructed samples into the baseline standard $PAC$ learner achieves an $(\varepsilon, \delta)$ target generalization error, demonstrating that standard learnability implies two-source learnability.

### Part (b): Two-Source Learning Implies Standard PAC Learnability
Conversely, assume we possess an active learner designed for the two-source configuration. Given an unstructured i.i.d. training sample $S$ drawn from the global distribution $\mathcal{D}$, we route the data points into two filtered subsets:
$$S^+ = \{x_i \in S \mid f(x_i) = +1\} \quad \text{and} \quad S^- = \{x_i \in S \mid f(x_i) = -1\}$$
Applying the conditional two-source learner on these isolated sets generates a hypothesis $h \in \mathcal{H}$ ensuring that with probability at least $1 - \delta$:
$$\Pr_{x \sim \mathcal{D}^+}[h(x) \neq +1] \leq \varepsilon \quad \text{and} \quad \Pr_{x \sim \mathcal{D}^-}[h(x) \neq -1] \leq \varepsilon$$
Invoking the **Law of Total Probability**, the cumulative risk under the unified distribution $\mathcal{D}$ aggregates linearly:
$$\Pr_{x \sim \mathcal{D}}[h(x) \neq f(x)] = \mathcal{D}(\mathcal{X}^+) \cdot \Pr_{x \sim \mathcal{D}^+}[h(x) \neq +1] + \mathcal{D}(\mathcal{X}^-) \cdot \Pr_{x \sim \mathcal{D}^-}[h(x) \neq -1]$$
$$\leq \varepsilon \cdot \mathcal{D}(\mathcal{X}^+) + \varepsilon \cdot \mathcal{D}(\mathcal{X}^-) = \varepsilon(\mathcal{D}(\mathcal{X}^+) + \mathcal{D}(\mathcal{X}^-)) = \varepsilon \cdot 1 = \varepsilon$$
This formalizes the converse direction, proving that the two frameworks are completely computationally equivalent in terms of learnability.

---

## Folder Contents
* `two_source_learning_solution.tex`: Complete theoretical mathematical proofs and step-by-step derivations written in LaTeX.
* `two_source_learning_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
