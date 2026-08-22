# Stochastic Modelling in Finance — Key Pedagogical Takeaways
## MScFE 622 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: Ordinary Calculus vs. Ito Calculus & The Quadratic Variation Bonus
Consider integrating Brownian motion $\int_0^T W_t dW_t$.
- **Ordinary Calculus Intuition**: If $W_t$ were a smooth differentiable function $x(t)$, $\int_0^T x dx = \frac{1}{2} x(T)^2$.
- **Mechanical Failure Mode (Neglecting Ito's Correction)**:
  Brownian paths are non-differentiable everywhere and have non-zero quadratic variation $[W, W]_t = t$ almost surely. In differential shorthand, $(dW_t)^2 = dt$.
  Using left-endpoint Riemann-Stieltjes sums yields:

$$\int_0^T W_t dW_t = \frac{1}{2} W_T^2 - \frac{1}{2} T$$

  Ignoring the second-order Ito drift correction $-\frac{1}{2}T$ causes severe, systematic over-valuation of options and derivative contracts.

---

### Toy Example 2: Negative Rates in Vasicek vs. The CIR Feller Boundary Violation
Consider modeling short-term interest rates $r_t$:
- **Vasicek Model**: $dr_t = \kappa(\theta - r_t) dt + \sigma dW_t$.
  Because diffusion $\sigma$ is constant, $r_t$ is Gaussian and admits negative interest rates $r_t < 0$ with non-zero probability.
- **Cox-Ingersoll-Ross (CIR) Model**: Adds square-root diffusion $dr_t = \kappa(\theta - r_t) dt + \sigma \sqrt{r_t} dW_t$.
- **Mechanical Failure Mode (Feller Condition Violation)**:
  If parameters violate the **Feller Condition** ($2\kappa\theta \le \sigma^2$), the origin $r = 0$ is an attainable boundary. Standard numerical discretization schemes attempt to evaluate $\sqrt{r_t}$ for negative values $r_t < 0$, throwing `NaN` runtime errors or causing square-root collapse in Monte Carlo path generation.

---

### Toy Example 3: Euler-Maruyama vs. Milstein Discretization Convergence
Consider simulating a state-dependent SDE $dX_t = \mu(X_t) dt + \sigma(X_t) dW_t$:
- **Euler-Maruyama Scheme**: $X_{n+1} = X_n + \mu(X_n)\Delta t + \sigma(X_n)\sqrt{\Delta t} Z_n$.
- **Mechanical Failure Mode (Poor Strong Convergence)**:
  Euler-Maruyama achieves a strong convergence order of only $\mathcal{O}(\sqrt{\Delta t})$ for state-dependent diffusions. For path-dependent derivatives (e.g., Barrier/Asian options), fine step sizes $\Delta t \to 0$ are computationally expensive.
- **Milstein Solution**:
  Adding the second-order Ito-Taylor expansion term $+\frac{1}{2}\sigma(X_n)\sigma'(X_n)[(\Delta W_n)^2 - \Delta t]$ restores strong convergence to $\mathcal{O}(\Delta t)$ without decreasing step size.

---

## 2. Core Mathematical Formulations & Evolution

### 1. Multi-Dimensional Ito's Lemma
For a scalar function $f(t, X_t)$ driven by SDE $dX_t = \mu_t dt + \sigma_t dW_t$:

$$df(t, X_t) = \left( \frac{\partial f}{\partial t} + \mu_t \frac{\partial f}{\partial X} + \frac{1}{2} \sigma_t^2 \frac{\partial^2 f}{\partial X^2} \right) dt + \sigma_t \frac{\partial f}{\partial X} dW_t$$

---

### 2. Ito Isometry
For any square-integrable adapted process $X_t$:

$$\mathbb{E}\left[ \left( \int_0^T X_t dW_t \right)^2 \right] = \mathbb{E}\left[ \int_0^T X_t^2 dt \right]$$

This converts complex stochastic expectations into deterministic time integrals.

---

### 3. Heston Stochastic Volatility SDE System

$$dS_t = \mu S_t dt + \sqrt{v_t} S_t dW_t^S$$

$$dv_t = \kappa(\theta - v_t) dt + \xi \sqrt{v_t} dW_t^v, \quad d\langle W^S, W^v \rangle_t = \rho dt$$

$$\text{Feller Condition for Positivity:} \quad 2\kappa\theta > \xi^2$$

---

### 4. Monte Carlo Variance Reduction (Control Variates)
To estimate $\theta = \mathbb{E}[X]$ using an analytical benchmark $Y$ with known expectation $\mathbb{E}[Y]$:

$$\hat{X}_{CV} = X - c^* (Y - \mathbb{E}[Y]), \quad c^* = \frac{\text{Cov}(X, Y)}{\text{Var}(Y)}$$

$$\text{Variance Reduction Ratio:} \quad \text{Var}(\hat{X}_{CV}) = \text{Var}(X) (1 - \rho_{XY}^2)$$

---

### 5. Eisenberg-Noe Financial Contagion Fixed Point
Systemic clearing payment vector $\mathbf{p}^*$ across interbank liability matrix $\mathbf{\Pi}$:

$$\mathbf{p}^* = \min\left( \bar{\mathbf{p}}, \; \mathbf{\Pi}^T \mathbf{p}^* + \mathbf{e} \right)$$

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Regime-Switching Tactical Asset Allocation (Gaussian HMM)
Fit a 3-State Gaussian Hidden Markov Model on VIX volatility dynamics to detect market regimes:
- **State 1 (Low Volatility)**: Allocate $100\%$ Equities (SPY).
- **State 2 (Medium Volatility)**: Allocate $50\%$ SPY / $50\%$ TLT.
- **State 3 (High Volatility / Panic)**: De-risk to $100\%$ Safe Haven (TLT / Cash).

### 2. Minimum Spanning Tree (MST) Correlation Filtering
Transform financial asset correlation matrix $\mathbf{\rho}$ into a Euclidean distance metric space $d_{ij} = \sqrt{2(1 - \rho_{ij})}$ and apply Kruskal's algorithm to extract systemic market backbones.

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Stochastic Model / Integrator | SDE / Numerical Formulation | Strong Convergence Order | Primary Advantage | Mechanical Failure Mode |
| :--- | :--- | :--- | :--- | :--- |
| **Geometric Brownian Motion (GBM)** | $dS_t = \mu S_t dt + \sigma S_t dW_t$ | Exact Analytical | Exact log-normal simulation | Constant volatility; flat implied vol surface |
| **Vasicek Short Rate** | $dr_t = \kappa(\theta - r_t) dt + \sigma dW_t$ | Exact Analytical | Mean-reverting Gaussian | Allows unrealistic negative interest rates |
| **Cox-Ingersoll-Ross (CIR)** | $dr_t = \kappa(\theta - r_t) dt + \sigma \sqrt{r_t} dW_t$ | Exact Non-Central $\chi^2$ | Non-negative short rates | Fails if Feller condition $2\kappa\theta > \sigma^2$ is violated |
| **Euler-Maruyama Scheme** | $X_{n+1} = X_n + \mu \Delta t + \sigma \sqrt{\Delta t} Z$ | $\mathcal{O}(\sqrt{\Delta t})$ | Simple to implement | Large discretization error for non-linear diffusions |
| **Milstein Scheme** | $X_{n+1} = \text{Euler} + \frac{1}{2}\sigma \sigma' ((\Delta W)^2 - \Delta t)$ | $\mathcal{O}(\Delta t)$ | Upgrades strong convergence order | Requires computing derivative of diffusion $\sigma'(X)$ |
| **Heston Stochastic Vol** | $dS = \mu S dt + \sqrt{v} S dW^S$ | Fourier Inverse / MC | Captures implied volatility skew & smiles | Complex calibration; 5 coupled parameters |
