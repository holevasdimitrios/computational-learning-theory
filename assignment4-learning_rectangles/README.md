# Assignment 4: Learning Axis-Aligned Rectangles & VC Dimension Bounds

## Problem Formulation
This assignment formalizes the sample complexity and combinatorial dimensions of the hypothesis class $\mathcal{H}_d$ consisting of axis-aligned hyperrectangles within $\mathbb{R}^d$. A point receives a $+1$ label if it is enclosed inside the targeted hyperrectangle and $-1$ otherwise.

The analysis is structured around four foundational components:
1. **ERM Characterization (a):** Proving that the algorithm which outputs the tightest, smallest bounding box wrapping around the positive training samples functions as an Empirical Risk Minimizer ($ERM$) in the realizable setting.
2. **PAC Sample Bound (b):** Demonstrating that this specific bounding box approach constitutes an $(\varepsilon, \delta)$-realizable $PAC$ learner with an optimal operational sample complexity of $\mathcal{O}(\frac{d}{\varepsilon} \log \frac{d}{\delta})$.
3. **VC Dimension Derivation (c):** Computing the exact Vapnik-Chervonenkis ($VC$) dimension of axis-aligned rectangles in $d$ dimensions, showing that $\text{VC}(\mathcal{H}_d) = 2d$.
4. **Generalization Complexity (d):** Contrast-checking the generic sample complexity upper bounds driven by the $VC$ dimension under both the strict *realizable* and relaxed *agnostic* $PAC$ environments.

---

## Theoretical Framework & Mathematical Proof Preview

### Part (a): The Bounding Box ERM Algorithm
Given a training sample $S$, let $R^*$ denote the true latent rectangle. The algorithm isolates all samples $x^{(j)}$ with $y^{(j)} = +1$ and computes the imperial empirical boundary markers along each dimension $i \in [d]$:
$$\hat{a}_i = \min \{ x_i^{(j)} : y^{(j)} = +1 \}, \quad \hat{b}_i = \max \{ x_i^{(j)} : y^{(j)} = +1 \}$$
Because the sample distribution is realizable ($S \subseteq R^*$), the estimated rectangle $\hat{R} = [\hat{a}, \hat{b}]$ is structurally nestled as a subset ($\hat{R} \subseteq R^*$). Consequently, no negative points slip into $\hat{R}$, and all positive points are contained by design, yielding a perfect empirical risk error score of zero ($L_S(h_{\hat{a}, \hat{b}}) = 0$), satisfying the definition of an $ERM$ mechanism.

### Part (b): Realizable PAC Analysis via Boundary Pruning
The generalization error $L_{\mathcal{D}}(h_{\hat{a}, \hat{b}})$ is bounded by the probability mass of the strips forming the symmetric difference $R^* \setminus \hat{R}$. This geometric margin can be decomposed into $2d$ boundary strips. For any dimension $i$, if the probability mass of a strip exceeds $\frac{\varepsilon}{2d}$, the probability that $m$ independent samples miss this strip entirely is at most:
$$\left(1 - \frac{\varepsilon}{2d}\right)^m \leq e^{-\frac{m\varepsilon}{2d}}$$
Applying the **Union Bound** across all $2d$ operational strips dictates that the overall generalization error stays safely under $\varepsilon$ with confidence $1 - \delta$, provided the operational sample complexity complies with:
$$m \geq \frac{2d}{\varepsilon} \ln\left(\frac{2d}{\delta}\right) \implies m_H^{\text{PAC}} = \mathcal{O}\left( \frac{d}{\varepsilon} \log \frac{d}{\delta} \right)$$

### Part (c): Generalizing the VC Dimension ($\text{VC} = 2d$)
* **Shattering Lower Bound ($\geq 2d$):** We can place $2d$ points on the axis lines of $\mathbb{R}^d$ close to the margins. By expanding or shrinking the axis-aligned intervals, any arbitrary dichotomy ($2^{2d}$ configurations of $+1$ and $-1$) can be precisely carved out, proving the class can shatter $2d$ items.
* **Shattering Upper Bound ($< 2d + 1$):** For any set of $2d + 1$ points, take the extreme points that define the minimal bounding box enclosing the set. This box is constrained by at most $2d$ points (the minimum and maximum along each of the $d$ coordinates). The remaining $(2d+1) - 2d = 1$ point must lie strictly inside this convex outer hull. It is physically impossible to assign a $-1$ label to this interior point while keeping the $2d$ outer boundary tracking points labeled as $+1$, preventing full shattering. Thus, $\text{VC}(\mathcal{H}_d) = 2d$.

### Part (d): Fundamental Sample Complexities
Applying fundamental statistical learning bounds tied directly to $\text{VC}(\mathcal{H}_d) = 2d$, the sample complex for generic tracking resolves to:
* **Realizable PAC Metric:** $m = \mathcal{O}\left( \frac{d}{\varepsilon} \log \frac{1}{\delta} \right)$
* **Agnostic PAC Metric:** $m = \mathcal{O}\left( \frac{d}{\varepsilon^2} \log \frac{1}{\delta} \right)$

---

## Folder Contents
* `learning_rectangles_solution.tex`: Complete theoretical mathematical proofs and step-by-step derivations written in LaTeX.
* `learning_rectangles_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
