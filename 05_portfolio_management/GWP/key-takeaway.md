# MScFE 652 Portfolio Management GWP 1 — Key Pedagogical Takeaways
## Empirical Factor Attribution & Robust Optimization Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: The Concentration Trap in Unconstrained Markowitz MVO
Consider constructing a portfolio from a 10-asset universe (TSLA, WMT, BAC, GS, LLY, MRK, GOOG, META, AAPL, XOM).
- **Unconstrained Optimizer Behavior**: Unconstrained Tangency optimization maximizes the sample Sharpe ratio:

$$\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}}$$

The solver identifies Walmart (WMT) and Goldman Sachs (GS) as having high sample mean returns relative to their variance/covariance, allocating **44.54% to WMT** and **35.85% to GS** (**80.39% concentrated in just 2 stocks**), while assigning **0.00% to 5 assets**.
- **Mechanical Failure Mode (Error Maximization & Out-of-Sample Fragility)**:
  In-sample, unconstrained MVO achieved a theoretical Sharpe ratio of $1.963$. However, in out-of-sample stress testing (Q4 2025), this hyper-concentrated portfolio suffered when market regimes shifted:
  - **Unconstrained OOS Cumulative Return**: $+8.41\%$
  - **Unconstrained OOS Max Drawdown**: $-4.78\%$
  - **Unconstrained OOS Sharpe Ratio**: $1.940$
- **The Concentration-Capped Solution ($0 \le w_i \le 0.18$)**:
  Imposing an $18\%$ maximum weight cap forced the optimizer to distribute capital across 7 assets and 5 distinct economic sectors. In out-of-sample backtesting, the constrained portfolio drastically outperformed:
  - **Constrained OOS Cumulative Return**: $+12.33\%$ ($+3.92\%$ excess return)
  - **Constrained OOS Max Drawdown**: $-2.92\%$ (nearly $2\%$ milder drawdown)
  - **Constrained OOS Sharpe Ratio**: $3.140$ ($+1.200$ Sharpe expansion)

---

### Toy Example 2: Outlier Sensitivity in OLS Factor Attribution vs Huber RLM
Consider regression of daily portfolio excess returns against the Fama-French 5 factors.
- **Ordinary Least Squares (OLS) Failure Mode**: OLS minimizes squared residual errors $\sum e_t^2$. On days with extreme earnings announcements or market shocks (e.g., a $4\sigma$ single-day return jump), squaring the error gives that single observation $16 \times$ the weight of a $1\sigma$ day. This skews factor betas $\boldsymbol{\beta}$ and inflates standard errors.
- **Huber Robust Regression (RLM) Solution**: Huber RLM replaces quadratic loss with a hybrid loss function $\rho_k(e)$ using tuning constant $k = 1.345 \sigma$. Outliers beyond $1.345\sigma$ are transition from $L_2$ quadratic penalty to $L_1$ linear penalty.
- **Empirical Impact**:
  - In OLS, Size factor SMB ($p = 0.1612$) and Profitability factor RMW ($p = 0.2848$) appear statistically insignificant.
  - In Huber RLM, downweighting heavy-tailed daily return outliers reveals that Size ($\text{SMB}, z = 1.78, p = 0.0746^{\star}$) and Profitability ($\text{RMW}, z = -1.69, p = 0.0909^{\star}$) are statistically significant factor drivers at the $10\%$ level.

---

## 2. Core Mathematical Formulations & Evolution

### 1. Portfolio Optimization Formulations

$$\begin{aligned}
\text{Step 1 (Unconstrained):} \quad &\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}} \quad \text{s.t.} \quad \sum_{i=1}^{10} w_i = 1, \quad w_i \ge 0 \\
\text{Step 2 (Constrained):} \quad &\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}} \quad \text{s.t.} \quad \sum_{i=1}^{10} w_i = 1, \quad 0 \le w_i \le 0.18
\end{aligned}$$

Selected Portfolio Weights (Step 2):

$$\mathbf{w}_{\text{Step 2}} = [\text{WMT}: 18.0\%, \text{BAC}: 18.0\%, \text{GS}: 18.0\%, \text{GOOG}: 18.0\%, \text{META}: 18.0\%, \text{LLY}: 9.05\%, \text{XOM}: 0.95\%]^T$$

---

### 2. Fama-French 5-Factor Regression Equation

$$R_{p, t} - R_{f, t} = \alpha + \beta_1 (R_{m, t} - R_{f, t}) + \beta_2 \text{SMB}_t + \beta_3 \text{HML}_t + \beta_4 \text{RMW}_t + \beta_5 \text{CMA}_t + \epsilon_t$$

---

### 3. Estimator Loss Functions & Robust Covariance

1. **OLS Loss & White (HC3) Heteroskedasticity-Consistent Variance**:

$$\hat{\boldsymbol{\beta}}_{\text{OLS}} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{Y}, \quad \text{Var}_{\text{HC3}}(\hat{\boldsymbol{\beta}}) = (\mathbf{X}^T \mathbf{X})^{-1} \left(\sum_{t=1}^T \frac{\hat{\epsilon}_t^2}{(1 - h_{tt})^2} \mathbf{x}_t \mathbf{x}_t^T \right) (\mathbf{X}^T \mathbf{X})^{-1}$$

where $h_{tt} = \mathbf{x}_t (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{x}_t^T$ is the leverage value for observation $t$.

2. **Huber $M$-Estimator Loss & Weighting**:

$$\rho_k(e) = \begin{cases} \frac{1}{2} e^2 & \text{if } |e| \le k \\ k |e| - \frac{1}{2} k^2 & \text{if } |e| > k \end{cases} \quad (k = 1.345 \sigma), \quad w(e_t) = \begin{cases} 1 & \text{if } |e_t| \le k \\ \frac{k}{|e_t|} & \text{if } |e_t| > k \end{cases}$$

Solved via Iteratively Reweighted Least Squares (IRLS): $\hat{\boldsymbol{\beta}}^{(m+1)} = \left(\mathbf{X}^T \mathbf{W}^{(m)} \mathbf{X}\right)^{-1} \mathbf{X}^T \mathbf{W}^{(m)} \mathbf{Y}$.

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Walk-Forward Chronological Data Partitioning

$$\begin{aligned}
\text{Training Window (In-Sample):} \quad &\text{2023-09-01 to 2025-09-30 } (N = 520 \text{ Trading Days}) \\
\text{Testing Window (Out-of-Sample):} \quad &\text{2025-10-01 to 2025-12-31 } (N = 63 \text{ Trading Days / Q4 2025})
\end{aligned}$$

**Methodological Rationale**:
- Prevents look-ahead bias and random shuffle data leakage in non-stationary time series.
- Evaluation on unobserved Q4 2025 market data validates out-of-sample stability.

---

### 2. Empirical Regression & Out-of-Sample Diagnostic Results

```
====================================================================================================
                        EMPIRICAL REGRESSION RESULTS & DIAGNOSTICS
====================================================================================================
Parameter / Metric         OLS Estimation (HC3)    Huber RLM Estimation    Interpretation
----------------------------------------------------------------------------------------------------
Annualized Alpha (α)       +32.81% (p = 0.0152 **) +28.98% (p = 0.0171 **) Statistically significant active alpha
Market Beta (Mkt-RF)       +0.0161 (p = 0.7801)    -0.0095 (p = 0.8342)    Market-neutral excess return posture
Size Beta (SMB)            +0.1244 (p = 0.1612)    +0.1193 (p = 0.0746 *)  RLM significant positive size tilt
Value Beta (HML)           +0.0540 (p = 0.5169)    +0.0244 (p = 0.7241)    Balanced value/growth neutrality
Profitability Beta (RMW)   -0.1299 (p = 0.2848)    -0.1718 (p = 0.0909 *)  Growth reinvestment vs static yield
Investment Beta (CMA)      -0.1217 (p = 0.3621)    -0.0983 (p = 0.3206)    Active capex & R&D deployment
----------------------------------------------------------------------------------------------------
In-Sample R²               0.0086 (0.86%)          --                      Pure active idiosyncratic return
In-Sample RMSE             0.01190                 --                      In-sample daily residual error
Out-of-Sample RMSE         0.00867                 --                      -27.1% error variance reduction OOS
Out-of-Sample R² (OOS)     -0.0408 (-4.08%)        --                      Orthogonal to passive factor indexes
====================================================================================================
Significance: ** p < 0.05, * p < 0.10
```

---

### 3. Institutional Governance & Rebalancing Architecture
- **Max Weight Boundary Ceiling**: Enforce $18.00\%$ asset cap at allocation.
- **Rebalancing Tolerance Band**: Semi-annual rebalancing triggered if any asset drifts past **$21.00\%$** ($+3\%$ buffer).
- **Risk Budgeting Benchmark**: Benchmark performance against an active multi-sector growth mandate rather than a broad market index, reflecting low systematic factor $R^2$ ($0.86\%$).

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Optimization / Econometric Model | Objective Function | Key Strengths | Fundamental Weaknesses | Primary Mathematical Tool |
| :--- | :--- | :--- | :--- | :--- |
| **Step 1: Unconstrained Tangency** | $\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}}$ | Theoretical maximum in-sample Sharpe ratio | Severe position concentration (80.39% in 2 stocks), high OOS drawdown | Analytic Matrix Inversion ($\mathbf{\Sigma}^{-1}$) |
| **Step 2: 18% Capped Tangency** | $\max_{\mathbf{w}} SR(\mathbf{w}) \text{ s.t. } 0 \le w_i \le 0.18$ | Forces sector diversification; superior OOS Sharpe (3.14) & low drawdown (-2.92%) | Boundary saturation at 18% cap | Quadratic Programming (QP / KKT Bounds) |
| **Factor Model OLS (HC3)** | $\min \sum e_t^2 \text{ with HC3 Var}$ | Unbiased parameter estimates under Gaussian errors; robust standard errors | Vulnerable to heavy-tailed return outliers ($e_t^2$ squaring leverage) | OLS & White HC3 Sandwich Estimator |
| **Factor Model Huber RLM** | $\min \sum \rho_k(e_t), k = 1.345\sigma$ | Downweights heavy-tailed daily outliers; reveals subtle factor loadings | Non-closed form; iterative algorithm convergence | Iteratively Reweighted Least Squares (IRLS) |
