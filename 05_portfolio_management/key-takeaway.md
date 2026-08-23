# Portfolio Management & Quantitative Risk — Key Pedagogical Takeaways
## MScFE 640 / 652 Master Quantitative Synthesis

[← Back to Main README.md](./README.md)

---

## 📖 Table of Contents & Quick Module Links
1. [Core Intuition & Mechanical Failure Modes](#1-core-intuition--mechanical-failure-modes)
   - [Toy Example 1: The 2-Asset Correlation & Leverage Trap](#toy-example-1-the-2-asset-correlation--leverage-trap)
   - [Toy Example 2: Compounding Drag & Asymmetric Loss Recovery](#toy-example-2-compounding-drag--asymmetric-loss-recovery)
   - [Toy Example 3: Behavioral Prospect Theory & Disposition Drag](#toy-example-3-behavioral-prospect-theory--disposition-drag)
2. [Core Mathematical Formulations & Calculus Derivations](#2-core-mathematical-formulations--calculus-derivations)
   - [1. Markowitz Lagrangian Matrix Optimization Derivation](#1-markowitz-lagrangian-matrix-optimization-derivation)
   - [2. Fama-French 5-Factor Huber Robust Regression Calculus](#2-fama-french-5-factor-huber-robust-regression-calculus)
   - [3. Kahneman-Tversky Prospect Theory Value Function Calculus](#3-kahneman-tversky-prospect-theory-value-function-calculus)
3. [Practical Engineering & Empirical GWP Results](#3-practical-engineering--empirical-gwp-results)
4. [Comparative Synthesis Cheat Sheet](#4-comparative-synthesis-cheat-sheet)

---

<a id="1-core-intuition--mechanical-failure-modes"></a>
## 1. Core Intuition & Mechanical Failure Modes

<a id="toy-example-1-the-2-asset-correlation--leverage-trap"></a>
### Toy Example 1: The 2-Asset Correlation & Leverage Trap

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Imagine trying to balance a seesaw with two people sitting on opposite ends. If they weigh different amounts and move randomly, you can offset their movements to stay flat (diversification). But if they both jump up and down in unison ($\rho \to 1.0$), any small tilt amplifies drastically, throwing you off the seesaw! 
Unconstrained mean-variance optimization (MVO) acts as an **error maximizer** when assets are highly correlated.

#### 🔢 Step-by-Step Numerical Calculation
Consider 2 stocks: Stock A ($\mu_A = 12\%, \sigma_A = 20\%$) and Stock B ($\mu_B = 8\%, \sigma_B = 15\%$).
Covariance Matrix $\mathbf{\Sigma}$ when correlation $\rho_{AB} = 0.98$:

$$\mathbf{\Sigma} = \begin{bmatrix} 0.0400 & 0.0294 \\ 0.0294 & 0.0225 \end{bmatrix}$$

Determinant $\det(\mathbf{\Sigma}) = (0.0400)(0.0225) - (0.0294)^2 = 0.0009 - 0.00086436 = 0.00003564 \approx 0$.
Inverting $\mathbf{\Sigma}^{-1}$:

$$\mathbf{\Sigma}^{-1} = \frac{1}{0.00003564} \begin{bmatrix} 0.0225 & -0.0294 \\ -0.0294 & 0.0400 \end{bmatrix} = \begin{bmatrix} 631.31 & -824.92 \\ -824.92 & 1122.33 \end{bmatrix}$$

Condition number $\kappa(\mathbf{\Sigma}) = \frac{\lambda_{\max}}{\lambda_{\min}} \approx 185.4$.
Plugging in noisy expected returns $\boldsymbol{\mu} = [0.12, 0.08]^T$ yields extreme unstable weights:

$$\mathbf{w}_{\text{unconstrained}} = \begin{bmatrix} +420\text{\%} \\ -320\text{\%} \end{bmatrix}$$

The optimizer demands $+420\%$ leverage in Stock A and $-320\%$ short position in Stock B over a tiny $0.01$ return noise error!

---

<a id="toy-example-2-compounding-drag--asymmetric-loss-recovery"></a>
### Toy Example 2: Compounding Drag & Asymmetric Loss Recovery

#### 💡 The Intuitive Metaphor (Easiest to Understand)
If you lose $50\%$ of your money on Day 1, you don't need a $50\%$ gain on Day 2 to get back to even—you need a **$+100\%$ gain** just to reach your starting point!

#### 🔢 Step-by-Step Calculation
- Start Capital: $\$100,000$.
- Period 1: $-50\%$ loss $\implies \$50,000$ remaining.
- Period 2: $+50\%$ gain $\implies \$50,000 \times 1.50 = \$75,000$ (Net loss of $-\$25,000$ or $-25\%$).
- Geometric mean return: $g = \sqrt{(1 - 0.50)(1 + 0.50)} - 1 = \sqrt{0.75} - 1 = 0.8660 - 1 = -13.40\%$ per period.
- Compounding Drag term $\approx \frac{1}{2}\sigma^2$: For $\sigma = 30\%$, volatility drag $= 0.5 \times (0.30)^2 = 4.5\%$ annual return penalty.

---

<a id="toy-example-3-behavioral-prospect-theory--disposition-drag"></a>
### Toy Example 3: Behavioral Prospect Theory & Disposition Drag

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Traders feel twice as much pain from losing $\$100$ as pleasure from gaining $\$100$. Because losing hurts so much, traders hold onto losing stocks hoping they'll get back to zero, while selling winning stocks early to lock in safety.

#### 🔢 Step-by-Step Calculation (Loss Aversion Multiplier)
Under Kahneman-Tversky Prospect Theory ($v(x)$):

$$v(x) = \begin{cases} x^{\alpha} & x \ge 0 \\ -\lambda (-x)^{\beta} & x < 0 \end{cases} \quad (\alpha = \beta = 0.88, \lambda = 2.25)$$

- Gain of $+\$1,000$: $v(+1000) = (1000)^{0.88} \approx +436.5$ units of utility.
- Loss of $-\$1,000$: $v(-1000) = -2.25 \times (1000)^{0.88} = -2.25 \times 436.5 = -982.1$ units of psychological pain.

---

<a id="2-core-mathematical-formulations--calculus-derivations"></a>
## 2. Core Mathematical Formulations & Calculus Derivations

<a id="1-markowitz-lagrangian-matrix-optimization-derivation"></a>
### 1. Markowitz Lagrangian Matrix Optimization Derivation
Minimizing portfolio variance subject to target return $\mu_0$ and full investment:

$$\min_{\mathbf{w}} \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} \quad \text{s.t.} \quad \mathbf{w}^T \boldsymbol{\mu} = \mu_0, \quad \mathbf{w}^T \mathbf{1} = 1$$

Lagrangian formulation:

$$\mathcal{L}(\mathbf{w}, \lambda_1, \lambda_2) = \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} - \lambda_1 (\mathbf{w}^T \boldsymbol{\mu} - \mu_0) - \lambda_2 (\mathbf{w}^T \mathbf{1} - 1)$$

Taking gradient vector derivative $\nabla_{\mathbf{w}} \mathcal{L} = \mathbf{0}$:

$$\mathbf{\Sigma} \mathbf{w} - \lambda_1 \boldsymbol{\mu} - \lambda_2 \mathbf{1} = \mathbf{0} \implies \mathbf{w}^{\star} = \mathbf{\Sigma}^{-1} (\lambda_1 \boldsymbol{\mu} + \lambda_2 \mathbf{1})$$

---

<a id="2-fama-french-5-factor-huber-robust-regression-calculus"></a>
### 2. Fama-French 5-Factor Huber Robust Regression Calculus
Huber Robust M-estimator loss function $\rho_\delta(e_i)$:

$$\rho_\delta(e_i) = \begin{cases} \frac{1}{2} e_i^2 & \text{if } |e_i| \le \delta \\ \delta |e_i| - \frac{1}{2}\delta^2 & \text{if } |e_i| > \delta \end{cases}$$

Derivative $\psi_\delta(e_i) = \frac{d\rho_\delta}{de_i}$:

$$\psi_\delta(e_i) = \begin{cases} e_i & |e_i| \le \delta \\ \delta \text{sgn}(e_i) & |e_i| > \delta \end{cases}$$

This bounds influence of market crisis outliers on factor beta estimations.

---

<a id="3-kahneman-tversky-prospect-theory-value-function-calculus"></a>
### 3. Kahneman-Tversky Prospect Theory Value Function Calculus
Marginal utility derivative $\frac{dv}{dx}$:

$$\frac{dv}{dx} = \begin{cases} \alpha x^{\alpha - 1} > 0 & x > 0 \text{ (Concave / Risk-Averse)} \\ \lambda \beta (-x)^{\beta - 1} > 0 & x < 0 \text{ (Convex / Risk-Seeking)} \end{cases}$$

---

<a id="3-practical-engineering--empirical-gwp-results"></a>
## 3. Practical Engineering & Empirical GWP Results

Empirical walk-forward factor regression results from `GWP`:
- **OLS Alpha**: $\alpha = +0.0018$ ($t = 1.45$, non-significant).
- **Huber Robust RLM Alpha**: $\alpha = +0.0021^{\star}$ ($t = 2.12$, significant after down-weighting outliers).

---

<a id="4-comparative-synthesis-cheat-sheet"></a>
## 4. Comparative Synthesis Cheat Sheet

| Optimization Model | Objective Function | Primary Strength | Mathematical Failure Mode |
| :--- | :--- | :--- | :--- |
| **Markowitz MVO** | $\min \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w}$ | Analytical efficiency frontier | Ill-conditioned inverse $\mathbf{\Sigma}^{-1}$ |
| **Black-Litterman** | $\boldsymbol{\mu}_{\text{BL}} = [(\tau \mathbf{\Sigma})^{-1} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{P}]^{-1} \dots$ | Combines market equilibrium with investor views | Sensitivity to confidence parameter $\tau$ |
| **Huber Robust RLM** | $\min \sum \rho_\delta(e_i)$ | Down-weights crisis return outliers | Non-linear iterative reweighting |
| **Hierarchical Risk Parity** | Tree clustering + Recursive bisection | Matrix-free allocation | Sensitive to cluster linkage choice |
