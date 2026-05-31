# Assignment 7: Worst-Case Hardness & Lower Bounds for the Perceptron Algorithm

## Problem Formulation
The classic Perceptron Convergence Theorem (Novikoff's Theorem) dictates that for any sequence of linearly separable samples bounded inside a sphere of radius $R$ and split by a target hyperplane with a geometric margin $\gamma$, the cumulative updates (mistakes) $M$ are upper-bounded by:
$$M \leq \frac{R^2 \cdot \|w^*\|^2}{\gamma^2}$$

The objective of this assignment is to construct a concrete mathematical configuration of $m$ points within $\mathbb{R}^3$ that forces the Perceptron algorithm to commit exactly $m$ consecutive mistakes under adversarial ordering, verifying that the worst-case upper bound is tight and achievable up to polynomial scaling.

---

## Theoretical Framework & Mathematical Proof Preview

### Adversarial Boundary Configuration
We position a sequence of $m$ instances $x_i = (a_i, b_i, y_i) \in \mathbb{R}^3$ matched with alternating conditional binary labels $y_i = (-1)^i$. We bound the quadratic radius constraints by forcing:
$$a_i^2 + b_i^2 = m^2 - 1$$

Evaluating the Euclidean vector norm for each point yields a uniform spherical shell distribution:
$$\|x_i\|^2 = a_i^2 + b_i^2 + y_i^2 = (m^2 - 1) + 1 = m^2 \implies R^2 = \max_i \|x_i\|^2 = m^2$$

Setting the underlying target weight matrix separator to $w^* = (0, 0, 1)$, the localized margin parameter $\gamma$ computes via inner products directly as:
$$\gamma = \min_i \frac{y_i (w^* \cdot x_i)}{\|w^*\|} = \min_i \frac{y_i \cdot y_i}{1} = 1$$

Thus, the theoretical maximum ceiling allowed by Novikoff's benchmark scales exactly to $M \leq m^2$.

### The Mistake Cascading Sequence
Starting from an initialized null vector $w^{(0)} = 0$, the operational weight update rule loops recursively after detecting an erroneous prediction sequence:
$$w^{(t)} = \sum_{j=1}^t y_j x_j$$

To guarantee that the incoming $(t+1)$-th point triggers a categorical misclassification block, the adversarial indexing coordinates are mapped sequentially via trigonometric distributions wrapped around a unit circle within the $(x_1, x_2)$ hyperplanes:
$$x_i = (\cos \theta_i, \sin \theta_i, y_i), \quad \text{where } \theta_i = \frac{2\pi i}{m} \text{ and } y_i = (-1)^i$$

This cyclic alternation forces the horizontal trajectory tracks to cancel each other out over the execution stream, keeping the projected projection length onto $w^*$ suppressed. This traps the algorithm into predicting the inverse label on every handshake, forcing a sequential update rate where $M = m$. 

Comparing the empirical error run $M = m$ against the upper bound ceiling $M \leq m^2$ proves that the analytical rate derived under margin separability constraints cannot be structurally improved without stricter spatial geometric conditions.

---

## Folder Contents
* `perceptron_lower_bound_solution.tex`: Complete theoretical mathematical proofs and step-by-step derivations written in LaTeX.
* `perceptron_lower_bound_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
