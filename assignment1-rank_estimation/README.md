# Assignment 1: Rank Estimation & Sample Complexity Bounds

## Problem Formulation
Given an unsorted list of distinct elements $x_1, x_2, \dots, x_n$, the objective is to randomly sample $m < n$ elements (with replacement) and return an element $x$ whose rank in the original list approximates a target value $k$, such that:

$$(1 - \varepsilon)k \leq \text{rank}(x) \leq (1 + \varepsilon)k$$

with a confidence probability of at least $1 - \delta$. The challenge is to define an optimal sampling strategy and derive the minimum sample complexity $m$ utilizing bounded notations ($\mathcal{O}$-notation).

---

## Theoretical Framework & Mathematical Proof Preview

### 1. Algorithmic Strategy
1. **Sampling:** Draw a random sample $S$ of size $m$ from the population with replacement.
2. **Sorting:** Sort the sample $S$ in descending order.
3. **Estimation:** Locate and return the element at index $\lfloor \frac{km}{n} \rfloor$ within the sorted sublist.

### 2. Analytical Error Bound via DKW Inequality
To guarantee that the empirical distribution function $F_m(x)$ closely tracks the true cumulative distribution $F(x)$, we invoke the **Dvoretzky-Kiefer-Wolfowitz (DKW) Inequality**:

$$\Pr \left[ \sup_{x} |F_m(x) - F(x)| > \varepsilon' \right] \leq 2e^{-2m(\varepsilon')^2}$$

Setting $\varepsilon' = \varepsilon \frac{k}{n}$, the sample complexity $m$ is analytically bounded by:

$$m \geq \frac{n^2}{2 \varepsilon^2 k^2} \ln \left( \frac{2}{\delta} \right)$$

Thus, the sample complexity scales as:

$$m = \mathcal{O}\left( \frac{n^2}{\varepsilon^2 k^2} \log \frac{1}{\delta} \right)$$

---

## Folder Contents
* `rank_estimation_solution.tex`: Complete analytical mathematical proofs and step-by-step derivations written in LaTeX.
* `rank_estimation_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
