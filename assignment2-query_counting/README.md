# Assignment 2: Query Counting & Population Estimation Bounds

## Problem Formulation
A hidden subset $S \subseteq \{1, \dots, n\}$ is maintained by an oracle. We can interact with the oracle by querying a set $Q \subseteq \{1, \dots, n\}$. The oracle returns a binary response indicating whether the intersection $S \cap Q$ is empty ($\emptyset$) or non-empty ($\neq \emptyset$). The objective is to efficiently estimate the cardinality of the hidden set $|S|$ with high confidence using a minimal number of queries.

This assignment explores three core questions:
1. **Decision Strategy (a):** Designing a query-based framework to distinguish whether $|S| \leq k$ or $|S| \geq (1+\varepsilon)k$ for any given threshold $k$.
2. **Cardinality Estimation (b):** Developing an efficient estimator $\hat{s}$ using bounded binary search routines such that $\hat{s} \leq |S| \leq (1+\varepsilon)\hat{s}$ holds with a probability of at least $2/3$, using logarithmic queries relative to $n$.
3. **Uniform Sampling (c):** Constructing an optimal randomized strategy to sample a uniform random element from the hidden set $S$ given its exact size $s = |S|$.

---

## Theoretical Framework & Mathematical Proof Preview

### Part (a): Stochastic Distinction Threshold
By advice, we construct a randomized subset $Q \subseteq \{1, \dots, n\}$ where each element $i$ is independently included in $Q$ with a sampling probability $p = 1/k$. We track the outcome using an indicator variable:
$$Z = \mathbb{I}[S \cap Q \neq \emptyset]$$
Letting $s = |S|$, the analytical probabilities for the boundary conditions dissolve into:
* **Case 1 ($s \leq k$):** $\Pr[Z = 1] \leq 1 - \left(1 - \frac{1}{k}\right)^k \leq 1 - \frac{1}{e}$
* **Case 2 ($s \geq (1+\varepsilon)k$):** $\Pr[Z = 1] \geq 1 - \left(1 - \frac{1}{k}\right)^{(1+\varepsilon)k} \geq 1 - \frac{1}{e^{1+\varepsilon}}$

The separation margin is given by a constant $c = \frac{1}{e^{1+\varepsilon}} - \frac{1}{e} = \Theta(\varepsilon)$. By repeating the query procedure $t$ times, we compute the empirical mean $\hat{p} = \frac{1}{t} \sum_{i=1}^t Z_i$. Invoking **Hoeffding's Inequality** with an error tolerance parameter $\alpha = c/2$, we evaluate the bound:
$$\Pr\left[|\hat{p} - \mathbb{E}[Z]| \geq \alpha \right] \leq 2e^{-2t\alpha^2}$$
To secure a confidence bound threshold of $1 - \delta$, the matching sample complexity of the decision routine resolves to:
$$t = \mathcal{O}\left( \frac{\log(1/\delta)}{\varepsilon^2} \right)$$

### Part (b): Stochastic Binary Search Framework
To optimize the estimation of $|S|$, we apply a binary search sequence over the operational domain $[1, n]$. At each logarithmic division step, we query the framework from Part (a) to prune the search space. 

To achieve a total failure probability bound of at most $1/3$ across the entire execution tree, we apply the **Union Bound** across the $\mathcal{O}(\log n)$ search steps by adjusting the local confidence parameter to $\delta = \frac{1}{3 \log n}$. Thus, the final composite query complexity scales optimally as:
$$\mathcal{O}\left( \frac{1}{\varepsilon^2} \log n \cdot \log\log n \right)$$

### Part (c): Exact Uniform Element Sampling
Given the exact knowledge of $s = |S|$, a customized subset $Q$ is populated using an independent operational inclusion parameter of $1/s$. The exact singular intersection probability satisfies:
$$\Pr[|S \cap Q| = 1] = s \cdot \frac{1}{s} \cdot \left(1 - \frac{1}{s}\right)^{s-1} \geq \frac{1}{e}$$
Since this structural intersection guarantees an isolated uniform point selection with a constant success chance, the expected replication overhead loop is strictly bounded by $\mathcal{O}(1)$. Once the singleton condition is met, recursive binary isolation steps over the active indices of $Q$ locate the targeted item with a localized overhead bound of $\mathcal{O}(\log n)$ oracle handshakes.

---

## Folder Contents
* `query_counting_solution.tex`: Complete theoretical mathematical proofs and step-by-step derivations written in LaTeX.
* `query_counting_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
