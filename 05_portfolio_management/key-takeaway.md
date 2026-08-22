# Portfolio Management & Quantitative Risk — Key Pedagogical Takeaways
## MScFE 640 / 652 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: The 2-Asset Correlation & Leverage Trap
Consider a 2-asset portfolio of Stock A ($\mu_A = 15\%, \sigma_A = 20\%$) and Stock B ($\mu_B = 10\%, \sigma_B = 15\%$). 
- **Naive Assumption**: If correlation $\rho_{AB} = 0$, equal weighting ($w = [0.5, 0.5]$) reduces portfolio variance to $\sigma_p^2 = 0.25(0.04) + 0.25(0.0225) = 0.0156 \implies \sigma_p = 12.5\%$.
- **Mechanical Failure Mode (Ill-Conditioned Covariance Inversion)**: In real markets, sample correlation matrices $\mathbf{\Sigma}$ are highly non-stationary and prone to multi-collinearity ($\rho_{AB} \to 0.98$). Unconstrained mean-variance optimization (MVO) inverts $\mathbf{\Sigma}$. As $\det(\mathbf{\Sigma}) \to 0$, the inverse $\mathbf{\Sigma}^{-1}$ explodes:

$$\mathbf{\Sigma}^{-1} = \frac{1}{\sigma_A^2 \sigma_B^2 (1 - \rho^2)} \begin{bmatrix} \sigma_B^2 & -\rho \sigma_A \sigma_B \\ -\rho \sigma_A \sigma_B & \sigma_A^2 \end{bmatrix}$$

The condition number $\kappa(\mathbf{\Sigma}) = \frac{\lambda_{\max}}{\lambda_{\min}}$ shoots from $\approx 1.8$ to $> 100$. The optimizer acts as an **error maximizer**, placing massive positive and negative bets (e.g., $w_A = +450\%, w_B = -350\%$) on minor estimation noise in expected returns $\boldsymbol{\mu}$.

---

### Toy Example 2: Compounding Drag & Asymmetric Loss Recovery
Consider a simple coin game with binary returns: $+50\%$ on heads, $-40\%$ on tails ($p = 0.5$).
- **Arithmetic Expected Return**: $E[R] = 0.5(0.50) + 0.5(-0.40) = +5.0\%$ per trade.
- **Mechanical Failure Mode (Compounding Drag)**: After two flips (1 heads, 1 tails), portfolio value is $(1 + 0.50)(1 - 0.40) = 1.50 \times 0.60 = 0.90$ (a **$-10\%$ net loss**).
- **Geometric Compound Return**: $g = \sqrt{(1.50)(0.60)} - 1 = \sqrt{0.90} - 1 \approx -5.13\%$ per period.
- **Asymmetry**: A $50\%$ drawdown requires a $+100\%$ return just to breakeven ($1 / (1 - 0.50) = 2.0$). Naive portfolio strategies ignoring volatility drag ($-\frac{1}{2}\sigma^2$) suffer compounding ruin despite positive arithmetic expected returns.

---

### Toy Example 3: Behavioral Prospect Theory & Disposition Drag
Consider a trader holding a winning stock (+$1,000$) and a losing stock ($-1,000$).
- **Traditional Utility Theory (Von Neumann-Morgenstern)**: Wealth $W$ is evaluated globally under a concave utility function $U''(W) < 0$. Risk aversion is symmetric.
- **Mechanical Failure Mode (The Reflection Effect)**: Humans evaluate gains/losses relative to a subjective reference point $R_0$. Under Kahneman-Tversky Prospect Theory:
  - In the gain domain ($x > 0$), investors are **risk-averse**, closing winners prematurely to lock in certainty ($v(x) = x^{0.88}$).
  - In the loss domain ($x < 0$), investors are **risk-seeking**, holding losers indefinitely expecting a rebound ($v(x) = -2.25(-x)^{0.88}$).
- **Empirical Failure**: Holding duration of losing trades far exceeds winning trades ($T_{\text{loss}} \gg T_{\text{win}}$). The disposition effect destroys long-term compounding by truncating right-tail gains and absorbing full left-tail drawdowns.

---

## 2. Core Mathematical Formulations & Evolution

### 1. Markowitz Quadratic Optimization $\to$ Tangency Portfolio
Classical MVO minimizes portfolio variance subject to a target expected return $\mu_0$ and full investment:

$$\min_{\mathbf{w}} \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} \quad \text{s.t.} \quad \mathbf{w}^T \boldsymbol{\mu} = \mu_0, \quad \mathbf{w}^T \mathbf{1} = 1$$

Formulating the Lagrangian with multipliers $\lambda_1, \lambda_2$:

$$\mathcal{L}(\mathbf{w}, \lambda_1, \lambda_2) = \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} - \lambda_1 (\mathbf{w}^T \boldsymbol{\mu} - \mu_0) - \lambda_2 (\mathbf{w}^T \mathbf{1} - 1)$$

Taking the gradient $\nabla_{\mathbf{w}} \mathcal{L} = \mathbf{\Sigma} \mathbf{w} - \lambda_1 \boldsymbol{\mu} - \lambda_2 \mathbf{1} = \mathbf{0}$, the optimal weights are:

$$\mathbf{w}^* = \lambda_1 \mathbf{\Sigma}^{-1} \boldsymbol{\mu} + \lambda_2 \mathbf{\Sigma}^{-1} \mathbf{1}$$

When a risk-free rate $r_f$ is introduced, the **Tangency Portfolio** maximizes the Sharpe Ratio:

$$\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}} \quad \text{s.t.} \quad \mathbf{w}^T \mathbf{1} = 1 \implies \mathbf{w}^*_{\text{tangency}} = \frac{\mathbf{\Sigma}^{-1}(\boldsymbol{\mu} - r_f \mathbf{1})}{\mathbf{1}^T \mathbf{\Sigma}^{-1}(\boldsymbol{\mu} - r_f \mathbf{1})}$$

---

### 2. Capital Asset Pricing Model (CAPM) $\to$ Fama-French 5-Factor Model
Equilibrium risk decomposition evolves from a single market factor to multi-factor fundamental drivers:

$$\text{CAPM:} \quad R_{i,t} - R_{f,t} = \alpha_i + \beta_{i,1} (R_{m,t} - R_{f,t}) + \epsilon_{i,t}, \quad \beta_{i,1} = \frac{\text{Cov}(R_i, R_m)}{\text{Var}(R_m)}$$

$$\text{FF5 Model:} \quad R_{i,t} - R_{f,t} = \alpha_i + \beta_{i,1}\text{Mkt}_t + \beta_{i,2}\text{SMB}_t + \beta_{i,3}\text{HML}_t + \beta_{i,4}\text{RMW}_t + \beta_{i,5}\text{CMA}_t + \epsilon_{i,t}$$

- $\text{SMB}_t$ (Small Minus Big): Size premium $\to$ compensates for small-cap illiquidity/distress.
- $\text{HML}_t$ (High Minus Low): Value premium $\to$ high book-to-market multiple mean-reversion.
- $\text{RMW}_t$ (Robust Minus Weak): Operating profitability spread derived from dividend discount model earnings.
- $\text{CMA}_t$ (Conservative Minus Aggressive): Investment factor $\to$ penalty on aggressive corporate capex expansion.

Covariance matrix factor decomposition reduces parameter noise from $\frac{N(N+1)}{2}$ to $N K + \frac{K(K+1)}{2}$:

$$\mathbf{\Sigma} = \mathbf{B} \mathbf{\Sigma}_F \mathbf{B}^T + \mathbf{D}$$

where $\mathbf{B}$ is the $N \times K$ factor loading matrix, $\mathbf{\Sigma}_F$ is the $K \times K$ factor covariance matrix, and $\mathbf{D}$ is the diagonal matrix of idiosyncratic variances $\sigma_{\epsilon, i}^2$.

---

### 3. The Black-Litterman Bayesian Master Equation
Black-Litterman resolves MVO error-maximization by blending an **equilibrium market prior** with **subjective investor views**:

1. **Market Equilibrium Prior**: Reverse-optimize implied excess returns $\boldsymbol{\Pi}$ from market-cap weights $\mathbf{w}_{\text{mkt}}$ and risk aversion parameter $\lambda = \frac{E[R_m] - r_f}{\sigma_m^2}$:

$$\boldsymbol{\Pi} = \lambda \mathbf{\Sigma} \mathbf{w}_{\text{mkt}}$$

2. **Subjective Views Matrix**: Express $K$ views as $\mathbf{P} \boldsymbol{\mu} = \mathbf{Q} + \boldsymbol{\epsilon}$, where $\boldsymbol{\epsilon} \sim \mathcal{N}(\mathbf{0}, \mathbf{\Omega})$.
3. **Master Bayesian Update**: Compute posterior mean $\bar{\boldsymbol{\mu}}_{BL}$ and covariance $\bar{\mathbf{\Sigma}}_{BL}$:

$$\bar{\boldsymbol{\mu}}_{BL} = \left[(\tau \mathbf{\Sigma})^{-1} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{P}\right]^{-1} \left[(\tau \mathbf{\Sigma})^{-1} \boldsymbol{\Pi} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{Q}\right]$$

$$\bar{\mathbf{\Sigma}}_{BL} = \mathbf{\Sigma} + \left[(\tau \mathbf{\Sigma})^{-1} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{P}\right]^{-1}$$

---

### 4. Critical Line Algorithm (CLA) & Karush-Kuhn-Tucker (KKT) Conditions
When real-world inequality constraints are added ($\mathbf{w}_{\min} \le \mathbf{w} \le \mathbf{w}_{\max}$), standard matrix inversions fail. The CLA (*Markowitz 1956, Bailey & López de Prado 2013*) solves exact piecewise-linear efficient frontiers using KKT optimality conditions:

$$\min_{\mathbf{w}} \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} - \gamma \mathbf{w}^T \boldsymbol{\mu} \quad \text{s.t.} \quad \mathbf{w}^T \mathbf{1} = 1, \quad l_i \le w_i \le u_i$$

$$\mathcal{L}(\mathbf{w}, \lambda, \boldsymbol{\lambda}_l, \boldsymbol{\lambda}_u) = \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} - \gamma \mathbf{w}^T \boldsymbol{\mu} - \lambda (\mathbf{w}^T \mathbf{1} - 1) - \boldsymbol{\lambda}_l^T (\mathbf{w} - \mathbf{l}) - \boldsymbol{\lambda}_u^T (\mathbf{u} - \mathbf{w})$$

The asset universe is partitioned into three sets: $\mathcal{F}$ (Free assets), $\mathcal{L}$ (Lower bounded assets), $\mathcal{U}$ (Upper bounded assets). As risk parameter $\gamma$ decreases, assets transition between bounds at exact discrete **turning points**, forming piecewise linear segments across corner portfolios.

---

### 5. Kahneman-Tversky Prospect Theory Value & Weighting Equations
1. **Asymmetric Value Function $v(x)$**:

$$v(x) = \begin{cases} x^\alpha & \text{if } x \ge 0 \\ -\lambda (-x)^\beta & \text{if } x < 0 \end{cases} \quad (\alpha = \beta \approx 0.88, \; \lambda \approx 2.25)$$

2. **Inverse S-Curve Probability Weighting Function $w(p)$**:

$$w(p) = \frac{p^\gamma}{\left(p^\gamma + (1-p)^\gamma\right)^{1/\gamma}} \quad (\gamma_{\text{gains}} \approx 0.61, \; \gamma_{\text{losses}} \approx 0.69)$$

Overweights rare tail risks ($p \to 0$), driving demand for lottery-like growth options and out-of-the-money protective put options.

---

### Mathematical Architecture & Optimization Trade-Offs

| Optimization Framework | Formulation / Objective Class | Computational Complexity | Global Convexity | Main Advantage | Critical Limitation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Unconstrained MVO** | Analytic Linear System | $\mathcal{O}(N^3)$ matrix inversion | Strictly Convex | Closed-form speed | Maximizes estimation error |
| **Constrained MVO (CLA)** | Quadratic Programming (QP) | $\mathcal{O}(N^3)$ per KKT transition | Convex | Handles exact box bounds | Non-stationary $\mathbf{\Sigma}$ inputs |
| **Black-Litterman** | Bayesian Conjugate Normal | $\mathcal{O}(N^3 + K^3)$ | Strictly Convex | Well-behaved stable weights | Sensitivity to scalar $\tau$ & $\mathbf{\Omega}$ |
| **Higher-Moment MVO** | Polynomial / Non-Convex | $\mathcal{O}(N^4)$ tensor operations | Non-Convex | Incorporates Skew/Kurtosis | Local minima traps |
| **Hierarchical Risk Parity** | Graph Tree Clustering (HRP) | $\mathcal{O}(N^2 \log N)$ hierarchical | Non-matrix inverse | No matrix inversion required | Sub-optimal if return signal is strong |

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Parameter Noise & Shrinkage Covariance Engineering
Sample covariance matrices $\mathbf{S}$ estimated over short time horizons ($T < 5N$) suffer from sample noise. **Ledoit-Wolf Shrinkage** computes an optimal linear combination of sample covariance $\mathbf{S}$ and a structured target matrix $\mathbf{F}$ (e.g., constant correlation model):

$$\mathbf{\Sigma}_{\text{shrunk}} = (1 - \delta) \mathbf{S} + \delta \mathbf{F}, \quad \delta^* = \frac{\sum \text{Var}(s_{ij})}{\sum (s_{ij} - f_{ij})^2}$$

This shrinks extreme eigenvalues toward the mean, reducing condition number $\kappa(\mathbf{\Sigma})$ by orders of magnitude and restoring numerical stability in quadratic solvers.

---

### 2. Machine Learning Extension: Hierarchical Risk Parity (HRP)
To completely bypass matrix inversion instability ($\mathbf{\Sigma}^{-1}$), López de Prado (2016) proposed **HRP**:
1. **Tree Clustering**: Compute distance matrix $d_{ij} = \sqrt{\frac{1 - \rho_{ij}}{2}}$. Apply Single/Ward Linkage hierarchical clustering to build a dendrogram tree.
2. **Quasi-Diagonalization**: Re-order assets in covariance matrix $\mathbf{\Sigma}$ so similar assets are adjacent.
3. **Recursive Bisection**: Split assets top-down, allocating inverse-variance weight to sub-clusters:

$$\alpha_1 = 1 - \frac{\sigma_1^2}{\sigma_1^2 + \sigma_2^2}, \quad w_i = w_i \times \alpha_1$$

---

### 3. Out-of-Sample Walk-Forward Stress Testing Framework
To prevent look-ahead bias and data leakage, backtests must strictly follow **walk-forward chronological validation**:

```
[--- Train Window: T_0 to T_1 ---][-- Test Window: T_1 to T_2 --]
                                 [--- Train Window: T_1 to T_2 ---][-- Test Window: T_2 to T_3 --]
```

- **Metrics to Track**: Out-of-Sample Sharpe Ratio ($SR_{\text{OOS}}$), Out-of-Sample $R^2_{\text{OOS}}$, Maximum Drawdown ($MDD$), Calmar Ratio ($CR = \frac{\mu}{MDD}$), tracking error variance.
- **Out-of-Sample $R^2$ Formula**:

$$R^2_{\text{OOS}} = 1 - \frac{\sum_{t \in \text{test}} (y_t - \hat{y}_t)^2}{\sum_{t \in \text{test}} (y_t - \bar{y}_{\text{train}})^2}$$

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Strategy / Method | Objective Function | Key Strengths | Fundamental Failure Modes / Weaknesses | Core Mathematical Tool |
| :--- | :--- | :--- | :--- | :--- |
| **Unconstrained Tangency MVO** | $\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}}$ | Maximum theoretical in-sample Sharpe ratio | Extreme weight volatility, error maximization, ill-conditioned matrix inversion | Linear Algebra ($\mathbf{\Sigma}^{-1}$) |
| **Constrained Tangency (Box Capped)** | $\max_{\mathbf{w}} SR(\mathbf{w}) \text{ s.t. } l_i \le w_i \le u_i$ | Enforces diversification, prevents single-asset blowups, superior OOS performance | Efficient frontier becomes piecewise non-linear; boundary saturation | Quadratic Programming (QP / KKT / CLA) |
| **Black-Litterman Model** | $\min_{\mathbf{w}} \frac{1}{2} \mathbf{w}^T \bar{\mathbf{\Sigma}}_{BL} \mathbf{w} - \lambda \mathbf{w}^T \bar{\boldsymbol{\mu}}_{BL}$ | Smooth, intuitive weights centered around equilibrium prior; incorporates user confidence | Sensitive to uncertainty calibration $\mathbf{\Omega}$ and scalar $\tau$ | Bayesian Conjugate Updating |
| **Fama-French 5-Factor OLS** | $\min_{\alpha, \boldsymbol{\beta}} \sum_{t=1}^T \epsilon_t^2$ | Decomposes return into systematic risk factors vs true stock-selection alpha | Sensitive to financial return fat-tail outliers ($e_t^2$ squaring penalty) | Ordinary Least Squares & White HC3 Robust Errors |
| **Huber Robust Regression (RLM)** | $\min_{\alpha, \boldsymbol{\beta}} \sum_{t=1}^T \rho_k(e_t)$ | Bounds outlier influence using hybrid $L_2/L_1$ loss function ($k = 1.345\sigma$) | Non-analytic closed form; requires iterative solution | Iteratively Reweighted Least Squares (IRLS) |
| **Hierarchical Risk Parity (HRP)** | Recursive Bisection Inverse-Variance | Eliminates matrix inversion; robust to severe correlation shocks | Ignores return expectations $\boldsymbol{\mu}$; purely risk-based allocation | Unsupervised Machine Learning (Tree Clustering) |
| **Behavioral Portfolio Theory (BPT)** | $\max V(\mathbf{w}) = \sum w(p_i) v(x_i)$ per mental layer | Matches real investor goal-based psychology; downside safety + aspirational growth | Fails to optimize global covariance; inefficient capital usage across layers | Prospect Theory Non-Linear Weighting Transformations |
| **Behaviorally Modified Allocation (BMAA)** | Advisor Matrix (SLR $\times$ Bias Type) | Prevents client panic selling by accommodating emotional non-critical preferences | Deviates from theoretical MPT efficient frontier | 2D Decision Scoring Matrix |
