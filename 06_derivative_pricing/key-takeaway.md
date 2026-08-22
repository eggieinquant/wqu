# Derivative Pricing — Key Pedagogical Takeaways
## MScFE 610 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: Real-World Drift $\mu$ vs. Risk-Neutral Pricing $\mathbb{Q}$ ($r$)
Consider pricing a 1-year European Call option ($K = \$100$) on two stocks, Stock A and Stock B, both with $S_0 = \$100$ and volatility $\sigma = 20\%$:
- Stock A has high expected return $\mu_A = 25\%$ (bullish biotech).
- Stock B has low expected return $\mu_B = 5\%$ (stable utility).
- **Naive Intuition**: Stock A is more likely to finish above $K = \$100$, so Call A should cost significantly more than Call B.
- **Mechanical Failure Mode (Violating Dynamic Replication)**:
  In an arbitrage-free market, a market maker dynamically hedges the option by shorting $\Delta = \frac{\partial C}{\partial S}$ shares of stock. This continuous rebalancing eliminates the stock's directional drift $\mu$ entirely.
- **Risk-Neutral Reality**:
  Both options have the exact same price:

$$C = f(S_0, K, T, r, \sigma)$$

  Option valuation depends purely on the risk-free rate $r$, not the real-world subjective drift $\mu$.

---

### Toy Example 2: The Black-Scholes Gamma-Theta Trade-off
Consider holding a Delta-neutral option portfolio ($\Pi = C - \Delta \cdot S$):
- **Core Mechanics**: For a delta-hedged portfolio, the continuous Black-Scholes PDE reduces to:

$$\Theta + \frac{1}{2} \sigma^2 S^2 \Gamma = r \Pi$$

- **Mechanical Failure Mode (The Long Volatility Trap)**:
  Buying option gamma ($\Gamma > 0$) provides positive convexity (you make money regardless of whether stock goes up or down). However, this convexity is not free: it is paid for every single day via continuous time-decay ($\Theta < 0$).
  Long volatility options lose money overall unless daily stock price moves exceed the market's implied volatility:

$$\text{Realized Volatility } \sigma_{\text{realized}} > \sigma_{\text{implied}}$$

---

### Toy Example 3: American Option Early Exercise Boundary (Puts vs. Calls)
Consider an American Put option ($K = \$100$) when underlying stock drops near zero ($S \to \$0.01$):
- **European Option Failure**: A European Put cannot be exercised until maturity $T$. Its value is $K e^{-rT}$.
- **American Option Early Exercise**: By exercising immediately at $t < T$, the holder receives cash $K = \$100$ today and earns interest at risk-free rate $r$.
- **Dynamic Programming Rule**: At each lattice node, compare immediate exercise value against continuation value:

$$V_n = \max\left( K - S_n, \; e^{-r\Delta t} \mathbb{E}^\mathbb{Q}[V_{n+1} \mid S_n] \right)$$

---

## 2. Core Mathematical Formulations & Evolution

### 1. Black-Scholes Partial Differential Equation (PDE)

$$\frac{\partial V}{\partial t} + (r - q) S \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} - r V = 0$$

---

### 2. Analytical Black-Scholes Formula & The Greeks

$$C(S, t) = S e^{-q\tau} \Phi(d_1) - K e^{-r\tau} \Phi(d_2), \quad P(S, t) = K e^{-r\tau} \Phi(-d_2) - S e^{-q\tau} \Phi(-d_1)$$

$$d_1 = \frac{\ln(S/K) + (r - q + \frac{1}{2}\sigma^2)\tau}{\sigma \sqrt{\tau}}, \quad d_2 = d_1 - \sigma \sqrt{\tau} \quad (\tau = T - t)$$

$$\text{Delta:} \; \Delta_C = e^{-q\tau} \Phi(d_1), \quad \text{Gamma:} \; \Gamma = \frac{e^{-q\tau} \phi(d_1)}{S \sigma \sqrt{\tau}}, \quad \text{Vega:} \; \mathcal{V} = S e^{-q\tau} \phi(d_1) \sqrt{\tau}$$

---

### 3. Lattice Pricing: CRR Binomial vs. Boyle Trinomial

$$\text{Binomial CRR:} \quad u = e^{\sigma \sqrt{\Delta t}}, \quad d = e^{-\sigma \sqrt{\Delta t}}, \quad p = \frac{e^{(r-q)\Delta t} - d}{u - d}$$

$$\text{Trinomial Boyle:} \quad u = e^{\lambda \sigma \sqrt{\Delta t}} \; (\lambda = \sqrt{3}), \quad d = 1/u, \quad m = 1$$

$$p_u = \frac{1}{2\lambda^2} + \frac{(r - q - \frac{1}{2}\sigma^2)\sqrt{\Delta t}}{2\lambda \sigma}, \quad p_d = \frac{1}{2\lambda^2} - \frac{(r - q - \frac{1}{2}\sigma^2)\sqrt{\Delta t}}{2\lambda \sigma}, \quad p_m = 1 - p_u - p_d$$

Trinomial trees achieve faster numerical convergence for American options by smoothing node parity oscillations.

---

### 4. Dupire Local Volatility Equation

$$\sigma_{\text{loc}}^2(K, T) = \frac{\frac{\partial C}{\partial T} + q C + K(r - q) \frac{\partial C}{\partial K}}{\frac{1}{2} K^2 \frac{\partial^2 C}{\partial K^2}}$$

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Implied Volatility Newton-Raphson Solver
Solve for implied volatility $\sigma_{\text{IV}}$ matching market price $C_{\text{market}}$:

$$\sigma_{n+1} = \sigma_n - \frac{C_{\text{BS}}(\sigma_n) - C_{\text{market}}}{\mathcal{V}(\sigma_n)}$$

If Vega $\mathcal{V} \to 0$ (deep OTM/ITM options), fallback to bisection root-finding to avoid divide-by-zero errors.

### 2. Longstaff-Schwartz Least-Squares Monte Carlo (LSM)
Price path-dependent American options by regressing OOS continuation values on basis functions (Laguerre polynomials) across in-the-money paths:

$$\mathbb{E}[V_{t+1} \mid S_t] = \sum_{k=0}^K a_k L_k(S_t)$$

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Derivative Pricing Scheme | Governing Engine | Primary Advantage | Convergence Rate | Primary Failure Mode |
| :--- | :--- | :--- | :--- | :--- |
| **Black-Scholes Analytical** | Continuous PDE exact solution | Instantaneous computation | Exact closed-form | Assumes constant volatility & zero jumps |
| **CRR Binomial Tree** | Discrete 2-branch lattice | Handles American early exercise | $\mathcal{O}(\Delta t)$ (oscillatory) | Node parity oscillations around strike $K$ |
| **Boyle Trinomial Tree** | Discrete 3-branch lattice | Higher stability & moment matching | $\mathcal{O}(\Delta t)$ (smooth) | Higher memory footprint $O(N^2)$ |
| **Explicit Finite Difference** | Forward time grid PDE solver | Simple matrix implementation | Conditionally stable | Unstable if $\Delta t > \frac{(\Delta S)^2}{\sigma^2}$ |
| **Implicit / Crank-Nicolson** | Tridiagonal linear solver | Unconditionally stable ($\theta = 0.5$) | $\mathcal{O}(\Delta t^2 + \Delta S^2)$ | Requires solving linear system $A x = b$ |
| **Longstaff-Schwartz LSM** | Monte Carlo + Cross-Sectional OLS | Prices high-dimensional American exotics | $\mathcal{O}(1/\sqrt{M})$ | Basis function mis-specification |
