# Assignment 3: Learning Distributions under Kolmogorov Distance

## Problem Formulation
This assignment investigates the sample complexity required to learn and verify arbitrary and monotone probability distributions over a discrete domain $[n]$ under the Kolmogorov distance and Total Variation distance.

The problem is analyzed through three core objectives:
1. **Distribution Learning (a):** Designing an algorithm that requires a sample complexity independent of the domain size $n$, scaling as $\mathcal{O}(\log(1/\varepsilon\delta)/\varepsilon^2)$ to approximate any distribution within a Kolmogorov distance of $\varepsilon$ with probability $1-\delta$.
2. **Minimax Lower Bound (b):** Proving that any learning algorithm under this framework strictly requires an information-theoretic lower bound of $\Omega(\log(1/\delta)/\varepsilon^2)$ samples.
3. **Monotone Property Testing (c):** Constructing an optimal tester to distinguish whether a known monotone (non-increasing) distribution $p$ is strictly uniform ($p = U_n$) or $\varepsilon$-far from uniform under the Total Variation distance ($d_{TV}(p, U_n) \geq \varepsilon$).

---

## Theoretical Framework & Mathematical Proof Preview

### Part (a): Distribution Agnostic Learning via DKW
Given $m$ i.i.d. samples $X_1, \dots, X_m \sim p$, we build the empirical cumulative distribution function (ECDF):
$$\hat{F}_m(i) = \frac{1}{m} \sum_{j=1}^m \mathbb{I}[X_j \leq i]$$
By invoking the **Dvoretzky-Kiefer-Wolfowitz (DKW) Inequality**, the supreme deviation between the empirical and true CDF is bounded non-asymptotically:
$$\Pr\left[ \sup_{i \in [n]} |\hat{F}_m(i) - F(i)| > \varepsilon \right] \leq 2e^{-2m\varepsilon^2}$$
Setting this failure probability bound to $\delta$ yields a sample complexity of $\mathcal{O}(\frac{\log(1/\delta)}{\varepsilon^2})$. This bound is fundamentally independent of $n$ because the Kolmogorov distance tracks the maximum vertical discrepancy between cumulative step functions, rather than evaluating individual probability mass errors across all coordinate dimensions.

### Part (b): Information-Theoretic Lower Bounds
The order-optimal lower bound $\Omega(\frac{\log(1/\delta)}{\varepsilon^2})$ is established by reducing the learning problem to a multiple hypothesis testing scenario over a hard pack of distributions. By applying **Le Cam’s Two-Point Method** or **Fano's Inequality**, we bound the minimax risk, proving that separating two candidate distributions spaced at least $\varepsilon$ apart under the Kolmogorov metric requires a sub-sampled statistical budget proportional to the mutual information expansion, confirming that the upper bound is tight.

### Part (c): Uniformity Testing under Monotonicity
For a non-increasing distribution ($p_{i+1} \leq p_{i}$), any significant deviation from uniformity ($d_{TV}(p, U_n) \geq \varepsilon$) heavily skews the boundary distributions at the endpoints $1$ and $n$. By estimating only $\hat{p}(1)$ and $\hat{p}(n)$ via sample frequencies, we construct a localized test statistic:
$$T = \left| \hat{p}(1) - \frac{1}{n} \right| + \left| \hat{p}(n) - \frac{1}{n} \right|$$
Applying **Hoeffding's Inequality** over these targeted boundary coordinates guarantees an optimal testing sample complexity of $\mathcal{O}(\frac{\log(1/\delta)}{\varepsilon^2})$, matching the minimax rate for property testing under monotonicity constraints.

---

## Folder Contents
* `kolmogorov_distance_solution.tex`: Complete theoretical mathematical proofs and step-by-step derivations written in LaTeX.
* `kolmogorov_distance_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
