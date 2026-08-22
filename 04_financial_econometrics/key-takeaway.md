# Financial Econometrics & Time Series Analysis — Key Pedagogical Takeaways
## MScFE 630 Master Quantitative Synthesis

[← Back to Main README.md](./README.md)

---

## 📖 Table of Contents & Quick Module Links
1. [Core Intuition & Mechanical Failure Modes](#1-core-intuition--mechanical-failure-modes)
   - [Toy Example 1: Spurious Regression & Non-Stationary Unit Roots](#toy-example-1-spurious-regression--non-stationary-unit-roots)
   - [Toy Example 2: Homoskedasticity Assumptions vs Volatility Clustering](#toy-example-2-homoskedasticity-assumptions-vs-volatility-clustering)
   - [Toy Example 3: Integer Differencing vs Fractional Differencing](#toy-example-3-integer-differencing-vs-fractional-differencing)
2. [Core Mathematical Formulations & Calculus Derivations](#2-core-mathematical-formulations--calculus-derivations)
   - [1. ARIMA(p,d,q) Characteristic Polynomial Roots](#1-arimapdq-characteristic-polynomial-roots)
   - [2. GARCH(1,1) Variance Half-Life Calculus](#2-garch11-variance-half-life-calculus)
   - [3. EGARCH Asymmetric Leverage Derivation](#3-egarch-asymmetric-leverage-derivation)
   - [4. Johansen VECM Cointegration Vector Decomposition](#4-johansen-vecm-cointegration-vector-decomposition)
3. [Practical Engineering & Cointegrated Statistical Arbitrage](#3-practical-engineering--cointegrated-statistical-arbitrage)
4. [Comparative Synthesis Cheat Sheet](#4-comparative-synthesis-cheat-sheet)

---

<a id="1-core-intuition--mechanical-failure-modes"></a>
## 1. Core Intuition & Mechanical Failure Modes

<a id="toy-example-1-spurious-regression--non-stationary-unit-roots"></a>
### Toy Example 1: Spurious Regression & Non-Stationary Unit Roots

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Suppose you record the cumulative height of a growing tree in Tokyo ($Y_t$) and the cumulative rainfall in London ($X_t$) over 10 years. Both numbers strictly increase over time. If you run a naive regression between them, your model will report a $99\%$ $R^2$ and claim London rain causes Tokyo tree growth! 
In econometrics, regressing two independent $I(1)$ random walks creates **Spurious Regression**—a false statistical illusion caused by shared non-stationary drift.

#### 🔢 Step-by-Step Numerical Calculation
- Series $Y_t = Y_{t-1} + \epsilon_t, \quad X_t = X_{t-1} + \eta_t, \quad \epsilon_t, \eta_t \sim \text{i.i.d. } \mathcal{N}(0, 1)$.
- Regressing $Y_t = \alpha + \beta X_t + u_t$ over $N = 1,000$ steps:
  - Estimated Slope: $\hat{\beta} = +0.85$
  - Standard Error: $\text{SE}(\hat{\beta}) = 0.04$
  - **t-statistic**: $t = \frac{0.85}{0.04} = 21.25 \implies p\text{-value} = 0.0000000000$
  - **$R^2$**: $0.88$ (Illusion of perfection!)
  - **Durbin-Watson Statistic**: $DW = 0.08 \ll 2.0$ (Severe residual autocorrelation!)

Because $DW \to 0$ as $N \to \infty$, standard OLS distribution theory breaks down entirely. The true slope is $\beta = 0$, but naive OLS rejects the true null hypothesis.

#### 📐 Calculus & Unit Root Proof
Let $L$ be the lag operator ($L Y_t = Y_{t-1}$). A process has a unit root if $(1 - L) Y_t = \epsilon_t$.
- Variance grows unbounded over time: $\operatorname{Var}(Y_t) = t \sigma_\epsilon^2 \xrightarrow{t \to \infty} \infty$.
- The asymptotic distribution of $\hat{\beta}$ does not follow Student-t, but rather a ratio of Wiener integrals:

$$\hat{\beta} \xrightarrow{d} \frac{\int_0^1 W_Y(r) W_X(r) dr}{\int_0^1 W_X(r)^2 dr}$$

Because the denominator does not collapse to a constant, $t$-statistics diverge to $\pm \infty$ at rate $\mathcal{O}(\sqrt{N})$.

---

<a id="toy-example-2-homoskedasticity-assumptions-vs-volatility-clustering"></a>
### Toy Example 2: Homoskedasticity Assumptions vs Volatility Clustering

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Assuming constant volatility in financial markets is like building a dam designed only for average sunny-day water levels. When a sudden storm hits, the dam breaks. **GARCH models** update their wall height dynamically based on yesterday's rain and storm intensity.

#### 🔢 Step-by-Step Calculation (GARCH(1,1) Volatility Update)
- Parameters: $\omega = 0.00001$, $\alpha = 0.10$ (shock sensitivity), $\beta = 0.85$ (persistence).
- Yesterday's variance: $\sigma_{t-1}^2 = 0.0002$ (daily volatility $= 1.41\%$).
- Yesterday's market crash shock: $\epsilon_{t-1} = -0.04$ (a $-4\%$ market drop).

**Updating Today's Variance $\sigma_t^2$**:

$$\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2 = 0.00001 + 0.10 \times (-0.04)^2 + 0.85 \times (0.0002)$$

$$\sigma_t^2 = 0.00001 + 0.10 \times 0.0016 + 0.00017 = 0.00001 + 0.00016 + 0.00017 = 0.00034$$

$$\text{Today's Updated Daily Volatility:} \quad \sigma_t = \sqrt{0.00034} = 1.8439\% \quad (\text{a } +30.4\% \text{ volatility spike!})$$

---

<a id="toy-example-3-integer-differencing-vs-fractional-differencing"></a>
### Toy Example 3: Integer Differencing vs Fractional Differencing

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Integer differencing ($d=1$) is like using a sledgehammer to remove noise—you smash away all long-term memory of past price levels. **Fractional Differencing ($d=0.35$)** is like using a fine scalpel: it removes just enough non-stationary trend to satisfy stationarity while preserving memory.

#### 🔢 Step-by-Step Expansion Calculation
Binomial expansion of $(1-L)^{0.35}$ for weights $w_k$:

$$w_0 = 1.0, \quad w_1 = -d = -0.35, \quad w_2 = \frac{d(1-d)}{2!} = \frac{0.35(0.65)}{2} = +0.11375$$

$$w_3 = -\frac{d(1-d)(2-d)}{3!} = -\frac{0.35 \times 0.65 \times 1.65}{6} = -0.06256$$

---

<a id="2-core-mathematical-formulations--calculus-derivations"></a>
## 2. Core Mathematical Formulations & Calculus Derivations

<a id="1-arimapdq-characteristic-polynomial-roots"></a>
### 1. ARIMA(p,d,q) Characteristic Polynomial Roots
$\Phi(L) = 1 - \phi_1 L - \dots - \phi_p L^p = 0$. Stationary requires all roots to lie strictly outside the complex unit circle $|z| > 1$.

---

<a id="2-garch11-variance-half-life-calculus"></a>
### 2. GARCH(1,1) Variance Half-Life Calculus

$$\text{Long-Run Variance:} \quad \bar{\sigma}^2 = \frac{\omega}{1 - \alpha - \beta}$$

Taking expected value $k$ steps ahead: $\mathbb{E}[\sigma_{t+k}^2] - \bar{\sigma}^2 = (\alpha + \beta)^k (\sigma_t^2 - \bar{\sigma}^2)$.
Setting deviation to half ($0.50$):

$$\tau_{1/2} = \frac{\ln(0.5)}{\ln(\alpha + \beta)}$$

For $\alpha + \beta = 0.95$: $\tau_{1/2} = \frac{-0.69315}{\ln(0.95)} = \frac{-0.69315}{-0.05129} \approx 13.5 \text{ trading days}$.

---

<a id="3-egarch-asymmetric-leverage-derivation"></a>
### 3. EGARCH Asymmetric Leverage Derivation

$$\ln(\sigma_t^2) = \omega + \beta \ln(\sigma_{t-1}^2) + \alpha |z_{t-1}| + \gamma z_{t-1}$$

Taking derivative with respect to standardized innovation $z_{t-1}$:

$$\frac{\partial \ln \sigma_t^2}{\partial z_{t-1}} = \begin{cases} \alpha + \gamma & \text{if } z_{t-1} > 0 \text{ (Good News)} \\ -\alpha + \gamma & \text{if } z_{t-1} < 0 \text{ (Bad News)} \end{cases}$$

If $\gamma < 0$, negative return shocks increase log-volatility far more than positive shocks of identical size.

---

<a id="4-johansen-vecm-cointegration-vector-decomposition"></a>
### 4. Johansen VECM Cointegration Vector Decomposition

$$\Delta \mathbf{Y}_t = \boldsymbol{\mu} + \mathbf{\Pi} \mathbf{Y}_{t-1} + \sum_{i=1}^{p-1} \mathbf{\Gamma}_i \Delta \mathbf{Y}_{t-i} + \boldsymbol{\epsilon}_t, \quad \mathbf{\Pi} = \boldsymbol{\alpha} \boldsymbol{\beta}^T$$

---

<a id="3-practical-engineering--cointegration-statistical-arbitrage"></a>
## 3. Practical Engineering & Cointegrated Statistical Arbitrage

### Pairs Trading Execution Loop
1. Johansen Rank test $\to \text{Rank}(\mathbf{\Pi}) = 1$. Cointegrating vector $\boldsymbol{\beta} = [1, -1.45]^T$.
2. Residual spread $S_t = Y_t - 1.45 X_t$.
3. Compute $Z_t = \frac{S_t - \mu_S}{\sigma_S}$. Enter when $|Z_t| > 2.0$.

---

<a id="4-comparative-synthesis-cheat-sheet"></a>
## 4. Comparative Synthesis Cheat Sheet

| Model / Framework | Primary Mathematical Identity | Target Volatility / Mean Dynamics | Key Stationarity Constraint | Primary Failure Mode |
| :--- | :--- | :--- | :--- | :--- |
| **ARIMA(p,d,q)** | $\Phi(L)(1-L)^d y_t = \Theta(L)\epsilon_t$ | Stationary mean forecasting | Roots outside unit circle | Assumes constant variance |
| **GARCH(1,1)** | $\sigma_t^2 = \omega + \alpha \epsilon_{t-1}^2 + \beta \sigma_{t-1}^2$ | Symmetric volatility clustering | $\alpha + \beta < 1$ | Blind to negative leverage effect |
| **EGARCH(1,1)** | $\ln \sigma_t^2 = \omega + \beta \ln \sigma_{t-1}^2 + \alpha|z| + \gamma z$ | Asymmetric leverage volatility | Unconstrained ($\ln \sigma^2 > 0$) | Optimization convergence sensitivity |
| **VECM Cointegration** | $\Delta \mathbf{Y}_t = \boldsymbol{\mu} + \boldsymbol{\alpha}\boldsymbol{\beta}^T \mathbf{Y}_{t-1} + \dots$ | Multivariable equilibrium spread | Spread $\boldsymbol{\beta}^T \mathbf{Y}_t \sim I(0)$ | Structural break in spread vector $\boldsymbol{\beta}$ |
