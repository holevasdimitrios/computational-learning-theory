# Assignment 6: Parameter Estimation via Projected SGD for Truncated Statistics

## Problem Formulation
This assignment addresses the foundational challenge of parametric distribution learning under geometric constraints, specifically focused on a Truncated Gaussian distribution. We consider a latent normal profile $\mathcal{N}(\mu^*, 1)$ with an unknown mean parameter satisfying $|\mu^*| \leq B$. Instead of observing unconstrained samples, we only receive truncated non-negative realizations $x \geq 0$ drawn directly from the conditional density $\mathcal{N}_{\geq 0}(\mu^*, 1)$.

The objective is to formulate a loss minimization problem based on the Negative Log-Likelihood ($NLL$), verify its structural optimization properties, and analyze the convergence complexity of a Projected Stochastic Gradient Descent ($Projected\ SGD$) estimator.

---

## Theoretical Framework & Mathematical Proof Preview

### Loss Minimization & Objective Function
To reconstruct the true mean parameter $\mu^*$, we minimize the expected negative log-likelihood of the truncated density wrapper with respect to our operational variable $\mu$:
$$f(\mu) = \mathbb{E}_{x \sim \mathcal{N}_{\geq 0}(\mu^*, 1)} \left[ -\log \left( \frac{e^{-\frac{1}{2}(x - \mu)^2}}{\int_0^\infty e^{-\frac{1}{2}(z - \mu)^2} dz} \right) \right]$$

By expanding the log-fraction and shifting variables using the standard Gaussian CDF $\Phi(\mu) = \int_{-\infty}^\mu \frac{1}{\sqrt{2\pi}}e^{-t^2/2}dt$, the continuous loss profile reduces strictly to:
$$f(\mu) = \frac{1}{2} \mathbb{E}[(x - \mu)^2] + \log \Phi(\mu)$$

### Structural Geometry & Smoothness
Over the restricted parameter envelope $\mu \in [-B, B]$, the function exhibits pristine optimization geometry:
* **Continuity & Differentiability:** The objective consists of an algebraic quadratic error term combined with a smooth log-concave Gaussian integral score.
* **Strong Convexity:** The quadratic baseline establishes a uniform positive lower bound on the Hessian ($\nabla^2 f(\mu) \geq c > 0$), sealing the presence of a unique global minimum $\mu^*$.
* **Lipschitz Continuity of Gradients:** The derivative profiles are smoothly bounded without erratic peaks, establishing that the gradient mapping is $L$-Lipschitz differentiable, which guarantees stable convergence tracks during gradient updates.

### Projected SGD Optimization Loop
An unbiased stochastic estimator of the true analytical gradient is derived at each sampling step $t$ using a single independent observation $x_t$:
$$g_t = \nabla_\mu \left( \frac{1}{2}(x_t - \mu)^2 + \log \Phi(\mu) \right) = (\mu - x_t) + \frac{\phi(\mu)}{\Phi(\mu)}$$
where $\phi(\mu)$ tracks the standard normal PDF. To ensure the candidate solution never drifts outside the meaningful configuration bounds, we inject a hard Euclidean boundary projection step $\Pi_{[-B,B]}$:
$$\mu_{t+1} = \Pi_{[-B,B]}\left( \mu_t - \eta g_t \right)$$
$$\text{where } \Pi_{[-B,B]}(x) = \min\{\max\{x, -B\}, B\}$$

### Convergence Sample Complexity
Invoking the classic optimization limits of stochastic projection frameworks operating on strongly convex regimes with bounded gradient variance, the expected estimation error tracks as:
$$\mathbb{E}[|\mu_T - \mu^*|] \leq \varepsilon \quad \text{provided that} \quad T = \mathcal{O}\left( \frac{1}{\varepsilon^2} \right)$$
This verifies that we can reliably estimate the true parameters using an observation budget entirely decoupled from the original untruncated tail mass.

---

## Folder Contents
* `truncated_statistics_solution.tex`: Complete theoretical mathematical proofs and step-by-step derivations written in LaTeX.
* `truncated_statistics_solution.pdf`: Compiled production-ready publication document.
* `ΕΚΠΑ.png`: The official institutional logo of the National and Kapodistrian University of Athens, embedded dynamically into the document's header for formal academic branding.
