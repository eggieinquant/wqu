# Financial Econometrics & Time Series Analysis — Key Pedagogical Takeaways
## MScFE 630 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: Spurious Regression & The Non-Stationary Trap
Consider regressing Stock Price $Y_t$ on Stock Price $X_t$, where both assets are independent pure random walks:

$$Y_t = Y_{t-1} + \epsilon_t, \quad X_t = X_{t-1} + \eta_t, \quad \epsilon_t, \eta_t \sim \text{i.i.d. } \mathcal{N}(0, 1)$$

- **Naive Intuition**: Running standard OLS $Y_t = \alpha + \beta X_t + u_t$ will show a slope near zero ($\beta \approx 0$) with no statistical significance ($p > 0.05$).
- **Mechanical Failure Mode (Spurious Regression)**:
  Because both series are integrated of order 1 ($I(1)$), OLS violates ergodic stationary assumptions. Standard errors vanish, producing inflated $R^2 \to 1.0$, $t$-statistics $> 15.0$, and a Durbin-Watson statistic $DW \to 0$. The researcher falsely concludes a strong economic relationship exists where there is only shared non-stationary drift.
- **Solution**: Test series for unit roots (ADF test). Model stationary log-returns $r_t = (1-L) \ln P_t \sim I(0)$, or test for **cointegration** if pricing spreads are needed.

---

### Toy Example 2: Homoskedasticity Violations & The Volatility Clustering Shock
Consider predicting market risk using OLS under constant variance $\text{Var}(\epsilon_t) = \sigma^2$:
- **Real Market Behavior**: Financial shocks cluster in time (Mandelbrot: "large changes are followed by large changes").
- **Mechanical Failure Mode**: Standard OLS underestimates risk during high-volatility regimes (crashes) and overestimates risk during low-volatility regimes (calm). Value-at-Risk (VaR) bounds computed under OLS fail catastrophically during crisis periods.
- **GARCH Solution**: Model conditional variance dynamically: $\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2$.

---

### Toy Example 3: Integer vs. Fractional Differencing ($d=1$ vs. $d=0.35$)
Consider transforming non-stationary price series $P_t \sim I(1)$ into a stationary feature matrix for prediction:
- **Standard Integer Differencing ($d=1$)**: $r_t = P_t - P_{t-1}$.
  Achieves stationarity, but completely wipes out historical memory (long-range autocorrelations).
- **Mechanical Failure Mode (Information Loss)**:
  The model loses all long-term mean-reverting signals, degrading predictive power for horizon forecasting.
- **ARFIMA Fractional Solution**:
  Fractionally differencing with $d \in (0, 0.5)$ preserves maximum historical memory while satisfying stationarity tests ($p < 0.05$).

---

## 2. Core Mathematical Formulations & Evolution

### 1. General ARIMA(p, d, q) Formulation

$$\Phi(L) (1 - L)^d y_t = c + \Theta(L) \epsilon_t$$

$$\text{where } \Phi(L) = 1 - \sum_{i=1}^p \phi_i L^i, \quad \Theta(L) = 1 + \sum_{j=1}^q \theta_j L^j$$

---

### 2. GARCH & Asymmetric Volatility Dynamics

$$\text{Standard GARCH(1,1):} \quad \sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2 \quad (\text{Stationarity: } \alpha + \beta < 1)$$

$$\text{Long-Run Variance:} \quad \bar{\sigma}^2 = \frac{\omega}{1 - \alpha - \beta}, \quad \text{Half-Life:} \quad \tau_{1/2} = \frac{\ln(0.5)}{\ln(\alpha + \beta)}$$

$$\text{EGARCH(1,1) [Leverage Effect]:} \quad \ln(\sigma_t^2) = \omega + \beta \ln(\sigma_{t-1}^2) + \alpha \left|\frac{\epsilon_{t-1}}{\sigma_{t-1}}\right| + \gamma \frac{\epsilon_{t-1}}{\sigma_{t-1}}$$

If $\gamma < 0$, negative return shocks (bad news) generate larger volatility spikes than positive shocks of equal magnitude.

---

### 3. Johansen Vector Error Correction Model (VECM)

$$\Delta \mathbf{Y}_t = \boldsymbol{\mu} + \mathbf{\Pi} \mathbf{Y}_{t-1} + \sum_{i=1}^{p-1} \mathbf{\Gamma}_i \Delta \mathbf{Y}_{t-i} + \boldsymbol{\epsilon}_t$$

$$\text{Rank Factorization:} \quad \mathbf{\Pi} = \boldsymbol{\alpha} \boldsymbol{\beta}^T$$

- $\boldsymbol{\beta} \in \mathbb{R}^{k \times r}$: Cointegrating vectors (stationary linear combinations).
- $\boldsymbol{\alpha} \in \mathbb{R}^{k \times r}$: Error-correction speed of adjustment parameters ($\alpha < 0$ restores equilibrium).

---

### 4. ARFIMA Fractional Expansion

$$(1 - L)^d = \sum_{k=0}^\infty \frac{\Gamma(k - d)}{\Gamma(-d)\Gamma(k + 1)} L^k = 1 - dL - \frac{d(1-d)}{2!} L^2 - \dots$$

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Statistical Arbitrage Pairs Trading Engine
1. Test asset pair $(X_t, Y_t)$ for cointegration using Johansen rank test ($r \ge 1$).
2. Estimate stationary error spread $S_t = Y_t - \beta X_t \sim I(0)$.
3. Compute rolling $Z$-score $Z_t = \frac{S_t - \mu_S}{\sigma_S}$.
4. **Trading Rule**: Enter Short Spread (Short Y / Long X) when $Z_t > +2.0$; Enter Long Spread when $Z_t < -2.0$; Exit positions when $|Z_t| < 0.25$.

### 2. High-Frequency Realized Volatility Filtering
Compute non-parametric intraday realized volatility $RV_t = \sum_{i=1}^M r_{t, i}^2$. Filter microstructure noise (bid-ask bounce) using optimal 5-minute sampling grids.

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Time Series Model | Primary Equation | Target Dynamics | Stationarity Requirement | Key Failure Mode |
| :--- | :--- | :--- | :--- | :--- |
| **ARIMA(p, d, q)** | $\Phi(L)(1-L)^d y_t = \Theta(L)\epsilon_t$ | Conditional mean prediction | $y_t \sim I(0)$ after $d$ differences | Assumes constant variance $\sigma^2$ |
| **GARCH(1,1)** | $\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2$ | Volatility clustering | Covariance stationary ($\alpha + \beta < 1$) | Symmetric response to positive/negative shocks |
| **EGARCH(1,1)** | $\ln(\sigma_t^2) = \omega + \beta \ln \sigma_{t-1}^2 + \alpha |z| + \gamma z$ | Asymmetric leverage effect | Unconstrained ($\ln \sigma^2$ is positive) | Computationally sensitive QMLE optimization |
| **VAR(p)** | $\mathbf{Y}_t = \mathbf{c} + \sum \mathbf{\Phi}_i \mathbf{Y}_{t-i} + \boldsymbol{\epsilon}_t$ | Multivariate macro interactions | All variables must be $I(0)$ | Parameter explosion $k^2 p$ |
| **VECM** | $\Delta \mathbf{Y}_t = \boldsymbol{\mu} + \boldsymbol{\alpha}\boldsymbol{\beta}^T \mathbf{Y}_{t-1} + \dots$ | Cointegrated statistical arbitrage | Variables $I(1)$, spread $\boldsymbol{\beta}^T \mathbf{Y} \sim I(0)$ | Structural break in cointegrating vector $\boldsymbol{\beta}$ |
| **ARFIMA(p, d, q)** | $(1-L)^d y_t = \text{ARMA}$ | Long-memory processes | Fractionally integrated $0 < d < 0.5$ | Slow truncation of binomial expansion |
