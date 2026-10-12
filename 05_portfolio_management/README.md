# Portfolio Management & Quantitative Risk (MScFE 640 / 652)

This directory contains lecture notes, readings, quantitative frameworks, empirical implementations, and research papers for **Portfolio Management & Quantitative Risk**. The curriculum spans classical normative portfolio theory (Markowitz Mean-Variance Optimization, CAPM, Factor Models, Black-Litterman Bayesian allocation, Critical Line Algorithm), modern descriptive behavioral finance (Kahneman-Tversky Prospect Theory, Behavioral Portfolio Theory, Behaviorally Modified Asset Allocation, investor profiling, and empirical market anomalies), capital growth and risk parity paradigms (Continuous Kelly Criterion, Fractional Kelly, Merton log utility, Equal Risk Contribution ERC, Conic Relaxed Risk Parity, Partitional Medoid Clustering & Performance Proportional Allocation), cutting-edge machine learning factor engineering (Fama-MacBeth 2-step regressions, Smart Beta Crowding & 2007 Quant Meltdown Liquidity Spirals, Gu-Kelly-Xiu Comparative Machine Learning Asset Pricing, and Automatic Genetic Programming Factor Construction with Differentiable Kernels), and advanced information-theoretic, spectral, and graph-based portfolio optimization (Covariance Shrinkage [Ledoit-Wolf, Rao-Blackwell, OAS, Graphical Lasso], Random Matrix Theory [Marcenko-Pastur CREM Denoising & Market Detoning], Information-Theoretic Distance [Shannon Entropy, Mutual Information, Variation of Information Metric], Minimum Spanning Trees, and Marcos López de Prado's Hierarchical Risk Parity [HRP] with tree seriation and recursive bisection).

---

## 📚 Module Overview

- **Course Code**: MScFE 640 / 652
- **Primary Focus**: 
  - **Modules 1–3**: Modern Portfolio Theory (MPT), Capital Market Theory (CAPM, APT, Fama-French), Black-Litterman Bayesian asset allocation, exact constrained optimization (Critical Line Algorithm), and Probabilistic Scenario Optimization (PSO).
  - **Module 4**: Behavioral Finance (Bounded Rationality, Prospect Theory, Skewness Preference, Layered Mental Accounting, BMAA, Investor Typologies, and Market Bubbles/Crashes).
  - **Module 5**: Kelly Criterion & Risk Parity (Continuous-Time Merton log-utility, Fractional Kelly, Drawdown Mitigation, Equal Risk Contribution [ERC], Relaxed Risk Parity via Second-Order Conic Programming [SOCP], Partitional Medoid Clustering, Distance Matrices, and Genetic Performance Proportional Allocation [PPA]).
  - **Module 6**: Advances and Challenges in Factor Investing (Factor Zoo, $t \ge 3.0$ Snooping Hurdle, Fama-MacBeth 2-Step Regressions, Bayesianized P-Values & Odds, Smart Beta Herding, August 2007 Quant Meltdown & Liquidity Deleveraging Cascades, Gu-Kelly-Xiu Machine Learning Asset Pricing across Trees/Neural Networks, and Automatic Factor Construction via Pre-trained NNs and Differentiable Genetic Programming).
  - **Module 7**: Information Theory and Graphs for Improved Portfolios (Covariance Shrinkage: Ledoit-Wolf, Rao-Blackwell, Oracle Approximating Shrinkage [OAS], Minimum Covariance Determinant [MCD], Graphical Lasso; Enhanced Portfolio Optimization [EPO]; Random Matrix Theory [RMT], Marcenko-Pastur Distribution [MPD], Constant Residual Eigenvalue Method [CREM] Denoising, Market Mode De-Toning; Information Theory: Shannon Entropy, Kullback-Leibler Divergence, Jaynes' Maximum Entropy Principle, Mutual Information [MI], Variation of Information [VI] Metric Distance, Stock Correlation Networks / Minimum Spanning Trees [MST]; and Hierarchical Risk Parity [HRP]: Optimal Number of Clusters [ONC], Quasi-Diagonalization Seriation, Recursive Bisection, and Hierarchical Equal Weight [HEW]).
  - **Module 8**: Better Backtesting and Reinforcement Learning (Overcoming Selection Bias under Multiple Testing [SBuMT], Seven Sins of Quantitative Investing, Bailey–López de Prado Expected Maximum Sharpe Ratio Hurdle, Probabilistic Sharpe Ratio [PSR], Deflated Sharpe Ratio [DSR]; Combinatorial Purged Cross-Validation [CPCV] with train purging and post-test embargoing; Reinforcement Learning Foundations [Markov Decision Process MDP, Bellman Optimality Equations, Value/Policy/Actor-Critic taxonomy, Policy Gradient Theorem]; and Live Practical Deep Reinforcement Learning Portfolio Allocation with FinRL [DDPG, TD3 with twin critics, PPO clipped surrogate objective, Soft Actor-Critic SAC with entropy temperature]).
  - **Group Work Projects (GWP1 & GWP2)**: 
    - **GWP1**: 10-asset portfolio optimization, rolling 3-factor and 5-factor Fama-French regressions, OLS vs Huber Robust RLM estimation, and beta stability.
    - **GWP2**: Machine learning portfolio optimization, Continuous/Constrained Kelly optimization ($20\%$ weight cap), Half-Kelly vs Double-Kelly tail risk profiling, K-fold cross-validation backtesting, RMT MPD Denoising, Market Detoning, Ledoit-Wolf Shrinkage, HRP vs HEW vs Tangency MVO.
- **Key Tools & Methodologies**: Quadratic programming, Second-Order Conic Programming (SOCP), convex optimization solvers, Bayesian conjugate updating, Quasi-Monte Carlo (Sobol low-discrepancy sequences), non-linear value/probability weighting transformations, Partitional Clustering (PAM, k-medoids, CLARA), Fama-MacBeth cross-sectional econometric passes, Huber robust M-estimators, Shallow & Deep Neural Networks with non-linear feature interactions, Tree-based Genetic Programming (Symbolic Regression with Soft-Rank Kernels), Random Matrix Theory (Marcenko-Pastur spectral clipping), Information Geometry (Variation of Information metric distance, Kruskal's MST algorithm), Hierarchical Tree Seriation & Recursive Bisection, Combinatorial Purged Cross-Validation (CPCV), and Deep Reinforcement Learning (PPO, TD3, SAC via FinRL).

---

> [!IMPORTANT]
> **🎓 Master Pedagogical Architecture & Key Takeaways**:
> Access the structured 5-pillar quantitative breakdown with worked numerical calculations, notation breakdowns, vector visualizations, and calculus derivations in **[`key-takeaway.md`](./key-takeaway.md)**:
> - 📐 **[Markowitz Matrix Inversion & Leverage Trap Math](./key-takeaway.md#toy-example-1-the-2-asset-correlation--leverage-trap)**
> - 📉 **[Compounding Volatility Drag & Asymmetric Recovery](./key-takeaway.md#toy-example-2-compounding-drag--asymmetric-loss-recovery)**
> - 🧠 **[Prospect Theory Value Function Calculus](./key-takeaway.md#3-kahneman-tversky-prospect-theory-value-function-calculus)**
> - 🎰 **[Kelly Growth Rate vs Over-Leverage Trap](./key-takeaway.md#toy-example-4-the-kelly-criterion-leverage-trap--half-kelly-optimality)**
> - 🌊 **[2007 Quant Meltdown & Crowded Deleveraging Spirals](./key-takeaway.md#toy-example-5-the-2007-quant-meltdown-crowded-trade--deleveraging-spiral)**
> - 📊 **[Random Matrix Theory Eigenvalue Noise & Small-Eigenvalue Inversion Trap](./key-takeaway.md#toy-example-6-random-matrix-theory-eigenvalue-noise--the-small-eigenvalue-inversion-trap)**
> - 🌳 **[Hierarchical Risk Parity vs MVO Quadratic Instability](./key-takeaway.md#toy-example-7-hierarchical-risk-parity-vs-mvo-quadratic-instability)**
> - 🎲 **[Multiple-Testing SBuMT Trap & Deflated Sharpe Ratio Math](./key-takeaway.md#toy-example-8-the-multiple-testing-sbumt-trap--deflated-sharpe-ratio)**
> - ⚖️ **[Equal Risk Contribution (ERC) & Log-Barrier Calculus](./key-takeaway.md#4-equal-risk-contribution-erc-risk-parity--log-barrier-calculus)**
> - 🧪 **[Fama-MacBeth 2-Step Regression & Shanken EIV Calculus](./key-takeaway.md#5-fama-macbeth-2-step-cross-sectional-regression--shanken-eiv-calculus)**
> - 🧬 **[Differentiable Soft-Rank Kernel in Automatic Factor Construction](./key-takeaway.md#6-differentiable-soft-rank-kernel-calculus-in-genetic-factor-construction)**
> - 🔬 **[Marcenko-Pastur Distribution & RMT Denoising/Detoning Calculus](./key-takeaway.md#7-marcenko-pastur-distribution--random-matrix-theory-rmt-denoising-calculus)**
> - 🌐 **[Information-Theoretic Distance & Variation of Information Metric Calculus](./key-takeaway.md#8-information-theoretic-distance--variation-of-information-metric-calculus)**
> - 🌲 **[Hierarchical Risk Parity (HRP) Recursive Bisection Calculus](./key-takeaway.md#9-hierarchical-risk-parity-hrp-recursive-bisection--inverse-variance-allocation-calculus)**
> - 📉 **[Deflated Sharpe Ratio & Combinatorial Purged Cross-Validation (CPCV) Calculus](./key-takeaway.md#10-deflated-sharpe-ratio-dsr--combinatorial-purged-cross-validation-cpcv-mathematics-module-8)**
> - 🤖 **[Deep Reinforcement Learning & Continuous Policy Gradient Calculus](./key-takeaway.md#11-deep-reinforcement-learning-continuous-control--policy-gradient-calculus-in-portfolio-management-module-8)**
> - 🏆 **[Empirical GWP2 Machine Learning Portfolio Benchmark](./key-takeaway.md#empirical-gwp2-machine-learning-portfolio-benchmark)**
> - 🚀 **[Empirical FinRL Deep Reinforcement Learning Portfolio Benchmark](./key-takeaway.md#empirical-finrl-deep-reinforcement-learning-portfolio-benchmark)**
> - 📚 **[Comprehensive Variable & Notation Glossary](./key-takeaway.md#5-comprehensive-mathematical-notation--variable-glossary)**

---

## 🏷️ Master Quantitative Notation & Variable Glossary

| Variable / Notation | Mathematical / Financial Meaning | Typical Units / Range | Context & Governing Formula |
| :--- | :--- | :--- | :--- |
| **$\mathbf{w}, w_i$** | Portfolio Allocation Weight Vector & Weight on Asset $i$ | $\sum w_i = 1.0$ | Budget constraint: $\mathbf{w}^T\mathbf{1} = \sum_{i=1}^N w_i = 1$ |
| **$\boldsymbol{\mu}, \mu_i$** | Expected Return Vector & Asset $i$ Expected Return | Annualized percentage | Portfolio expected return: $\mathbb{E}[R_p] = \mathbf{w}^T\boldsymbol{\mu}$ |
| **$\mu_0$** | Target Portfolio Return Constraint | Annualized percentage | Mean-variance constraint: $\mathbf{w}^T\boldsymbol{\mu} = \mu_0$ |
| **$\mathbf{\Sigma}$** | Asset Covariance Matrix ($N \times N$) | Covariance units | $\sigma_p^2 = \mathbf{w}^T\mathbf{\Sigma}\mathbf{w}$; condition number $\kappa(\mathbf{\Sigma})$ dictates inversion stability |
| **$\mathbf{S}, \mathbf{C}$** | Sample Covariance Matrix & Sample Correlation Matrix | Real symmetric matrices | $\mathbf{C} = \text{diag}(\mathbf{S})^{-1/2} \mathbf{S} \text{diag}(\mathbf{S})^{-1/2}$ |
| **$\sigma_p(\mathbf{w})$** | Total Portfolio Standard Deviation / Risk | Annualized percentage | Euler's homogeneity decomposition: $\sigma_p = \sum_{i=1}^N \text{RC}_i(\mathbf{w})$ |
| **$\text{MRC}_i$** | Marginal Risk Contribution of Asset $i$ | Rate of change ($\partial \sigma_p / \partial w_i$) | $\text{MRC}_i = \frac{\partial \sigma_p}{\partial w_i} = \frac{(\mathbf{\Sigma}\mathbf{w})_i}{\sigma_p}$ |
| **$\text{RC}_i$** | Total Risk Contribution of Asset $i$ | Risk units | $\text{RC}_i = w_i \times \text{MRC}_i$; Risk Parity equalizes $\text{RC}_i = \sigma_p / N$ |
| **$\lambda_1, \lambda_2$** | Lagrange Multipliers for Return and Budget Constraints | Shadow prices | Optimal analytical weights: $\mathbf{w}^\star = \mathbf{\Sigma}^{-1}(\lambda_1\boldsymbol{\mu} + \lambda_2\mathbf{1})$ |
| **$f, f^*$** | Portfolio Leverage Fraction & Full Kelly Optimum | Real scalar ($f^* = 2.0 = 2\times$) | Growth rate maximization: $f^* = \frac{\mu - r_f}{\sigma^2}$ |
| **$g(f)$** | Continuous Logarithmic Compounded Growth Rate | Annualized percentage | $g(f) = r_f + f(\mu - r_f) - \frac{1}{2}f^2\sigma^2$ |
| **$v(x)$** | Kahneman-Tversky Prospect Theory Value Function | Subjective utility units | $v(x) = x^\alpha$ (for $x \ge 0$) and $v(x) = -\lambda(-x)^\beta$ (for $x < 0$) |
| **$\lambda$** | Loss Aversion Multiplier | Calibration constant ($\lambda \approx 2.25$) | Psychological penalty factor ($\lambda \approx 2.25$) |
| **$\alpha, \beta$** | Prospect Theory Diminishing Sensitivity Exponents | Empirical scalars ($\alpha = \beta \approx 0.88$) | Concave in gains ($\alpha \approx 0.88$), convex in losses ($\beta \approx 0.88$) |
| **$\rho_\delta(e), \psi_\delta(e)$** | Huber Robust Loss Function & Influence Derivative | Bounded M-estimator ($\delta \approx 1.345$) | Robust factor regression: bounds crisis residual outliers |
| **$\hat{\boldsymbol{\beta}}_i, \hat{\mathbf{B}}$** | Factor Beta Loadings Vector & $N \times K$ Beta Matrix | Factor exposures | First pass time-series regression estimators |
| **$\boldsymbol{\lambda}_t, \bar{\boldsymbol{\lambda}}$** | Cross-Sectional Factor Risk Premia Vector & Time-Series Mean | Factor returns | Second pass cross-sectional regression estimators |
| **$\text{AsyVar}(\bar{\boldsymbol{\lambda}})$** | Shanken (1992) Errors-in-Variables (EIV) Covariance Matrix | Corrected asymptotic variance | Corrects for first-pass beta estimation noise in factor premia |
| **$\widetilde{\text{rank}}_\tau(x_i)$** | Differentiable Soft-Rank Kernel with Temperature $\tau$ | Continuous ranks $[1, N]$ | $\widetilde{\text{rank}}_\tau(x_i) = 1 + \sum_{j \ne i} \frac{1}{1 + e^{-(x_i - x_j)/\tau}}$ |
| **$L$** | Gross Portfolio Leverage Multiplier | Gross / Net Equity | Gross market exposure relative to net investor equity |
| **$q$** | Observation-to-Asset Matrix Ratio in RMT | $q = T / N \ge 1.0$ | Controls Marcenko-Pastur random noise spectral limits |
| **$\lambda_-, \lambda_+$** | Lower & Upper Marcenko-Pastur Noise Eigenvalue Limits | Positive real eigenvalues | $\lambda_\pm = \sigma^2 (1 \pm \sqrt{1/q})^2$ |
| **$p(\lambda)$** | Marcenko-Pastur Eigenvalue Probability Density Function | Probability density | $p(\lambda) = \frac{q}{2\pi \sigma^2 \lambda} \sqrt{(\lambda_+ - \lambda)(\lambda - \lambda_-)}$ |
| **$\mathbf{\Sigma}_{\text{shrunk}}$** | Ledoit-Wolf Linear Shrunken Covariance Matrix | Covariance units | $\mathbf{\Sigma}_{\text{shrunk}} = (1 - \delta^\star)\mathbf{S} + \delta^\star \mathbf{F}$ |
| **$\delta^\star$** | Optimal Ledoit-Wolf Shrinkage Intensity | $\delta^\star \in [0, 1]$ | Minimizes Expected Quadratic Frobenius Loss |
| **$\mathbf{C}_{\text{EPO}}$** | Pedersen Enhanced Portfolio Optimization Shrunken Correlation | Correlation units | $\mathbf{C}_{\text{EPO}} = (1 - w)\mathbf{C} + w \mathbf{I}$ |
| **$H(X), H(X, Y)$** | Marginal Shannon Entropy and Joint Entropy | Bits / Shannons ($H \ge 0$) | $H(X) = -\sum p(x)\log_2 p(x)$ |
| **$I(X; Y)$** | Mutual Information between Asset Returns $X$ and $Y$ | Bits / Shannons ($I \ge 0$) | $I(X; Y) = H(X) + H(Y) - H(X, Y)$ |
| **$VI(X, Y)$** | Variation of Information Metric Distance | Information units | $VI(X, Y) = H(X, Y) - I(X; Y) = H(X|Y) + H(Y|X)$ |
| **$\widetilde{VI}(X, Y)$** | Normalized Variation of Information Metric Distance | $\widetilde{VI} \in [0, 1]$ | $\widetilde{VI}(X, Y) = \frac{VI(X, Y)}{H(X, Y)}$ |
| **$\mathbf{D}, d_{i,j}$** | Angular Distance Matrix between Assets | $d_{i,j} \in [0, 1]$ | $d_{i,j} = \sqrt{\frac{1 - \rho_{i,j}}{2}}$ |
| **$\widetilde{V}_k$** | Cluster Variance of Sub-Tree Cluster $\mathcal{C}_k$ in HRP | Variance units | $\widetilde{V}_k = \mathbf{w}_k^T \mathbf{\Sigma}_k \mathbf{w}_k$ |
| **$\alpha^\star$** | HRP Optimal Recursive Bisection Split Multiplier | $\alpha^\star \in (0, 1)$ | $\alpha^\star = \frac{\widetilde{V}_2}{\widetilde{V}_1 + \widetilde{V}_2} = 1 - \frac{\widetilde{V}_1}{\widetilde{V}_1 + \widetilde{V}_2}$ |
| **$\kappa(\mathbf{\Sigma})$** | Matrix Condition Number | $\kappa = \lambda_{\max} / \lambda_{\min} \ge 1.0$ | Measures numerical matrix inversion instability |
| **$\text{CVaR}_{0.95}$** | $95\%$ Conditional Value at Risk (Expected Shortfall) | Percentage loss | $\mathbb{E}[R \mid R \le \text{VaR}_{0.95}]$ |
| **$N_{\text{trials}}$** | Total Number of Strategy Trials Tested | Positive integer | Used in SBuMT multiple testing correction |
| **$SR_0, \mathbb{E}[\max SR]$** | Expected Maximum Sharpe Ratio Hurdle under Null | Dimensionless ratio | $SR_0 \approx \sqrt{V[SR]} ((1-\gamma)Z^{-1}(1 - 1/N) + \gamma Z^{-1}(1 - 1/(Ne)))$ |
| **$\text{PSR}(SR^*)$** | Probabilistic Sharpe Ratio | Probability $[0, 1]$ | $\text{PSR}(SR^*) = Z\left(\frac{(\widehat{SR} - SR^*)\sqrt{T-1}}{\sqrt{1 - \hat{\gamma}_3 \widehat{SR} + \frac{\hat{\gamma}_4 - 1}{4}\widehat{SR}^2}}\right)$ |
| **$\text{DSR}$** | Deflated Sharpe Ratio | Probability $[0, 1]$ | $\text{DSR} = \text{PSR}(SR_0)$ |
| **$\gamma_{\text{Euler}}$** | Euler-Mascheroni Constant | $\approx 0.5772156649$ | Normalizing constant in Gumbel EVT limit |
| **$\hat{\gamma}_3, \hat{\gamma}_4$** | Strategy Return Sample Skewness and Kurtosis | Real scalars | Adjusts Sharpe standard error for fat tails and asymmetry |
| **$\phi$** | Number of Generated CPCV Backtest Paths | Positive integer | $\phi = \frac{k}{N}\binom{N}{k}$ |
| **$\mathbf{s}_t, \mathbf{a}_t$** | DRL State Vector and Action Allocation Vector | $\mathbf{s}_t \in \mathcal{S}, \mathbf{a}_t \in \Delta^{N-1}$ | MDP continuous state and allocation weights |
| **$r_t(\mathbf{s}_t, \mathbf{a}_t)$** | DRL Immediate Reward Function | Real scalar | $r_t = \mathbf{w}_t^T \mathbf{R}_t - \frac{\lambda_{\text{risk}}}{2}\sigma_{p,t}^2 - c_{\text{trans}}\|\mathbf{w}_t - \mathbf{w}_{t-1}\|_1$ |
| **$\pi_\theta(\mathbf{a} \mid \mathbf{s})$** | Parameterized Policy Network with Weights $\theta$ | Probability distribution / map | Action selection in continuous actor-critic DRL |
| **$V(\mathbf{s}), Q(\mathbf{s}, \mathbf{a})$** | State-Value Function & Action-Value Function | Expected cumulative reward | $V(\mathbf{s}) = \mathbb{E}[\sum \gamma^t r_t \mid \mathbf{s}_0 = \mathbf{s}]$ |
| **$A(\mathbf{s}, \mathbf{a})$** | Advantage Function | Reward units | $A(\mathbf{s}, \mathbf{a}) = Q(\mathbf{s}, \mathbf{a}) - V(\mathbf{s})$ |
| **$L^{\text{CLIP}}(\theta)$** | PPO Clipped Surrogate Loss Function | Loss units | Bounds destructive policy gradient updates |
| **$\epsilon_{\text{clip}}$** | PPO Policy Probability Ratio Clip Bound | Scalar ($\epsilon \approx 0.20$) | Clips probability ratio to $[1-\epsilon, 1+\epsilon]$ |
| **$\alpha_{\text{SAC}}$** | Soft Actor-Critic Entropy Temperature | Positive scalar | Trades off exploration entropy $\mathcal{H}(\pi)$ vs reward |

---

## 📊 Visual Frameworks & Architecture

### 1. Markowitz Efficient Frontier & Capital Allocation Line (CAL) — [*Detailed Math & Calculations in key-takeaway.md*](./key-takeaway.md#1-markowitz-lagrangian-matrix-optimization-derivation)

```mermaid
flowchart TD
    subgraph Asset_Universe ["Asset Universe & Covariance Matrix Σ"]
        A1["Asset 1: Equities"]
        A2["Asset 2: Fixed Income"]
        A3["Asset 3: Commodities / Alternatives"]
    end
    
    Asset_Universe --> MVO["Markowitz Quadratic Optimizer:\nmin w^T Σ w  s.t.  w^T μ = μ_0, w^T 1 = 1"]
    MVO --> EF["Efficient Frontier Curve (Parabolic Boundary)"]
    
    subgraph CAL_Optimization ["Tangency Portfolio & CAL"]
        Rf["Risk-Free Rate r_f"] --> Tangency["Max Sharpe Ratio Tangency Portfolio:\nmax (w^T μ - r_f) / sqrt(w^T Σ w)"]
        EF --> Tangency
        Tangency --> CAL["Capital Allocation Line (CAL):\nE[R_p] = r_f + SR * σ_p"]
    end
```

### 2. Black-Litterman Bayesian Master Allocation Workflow

```mermaid
flowchart TD
    subgraph Market_Equilibrium ["1. Market Equilibrium Prior"]
        Wmkt["Market Cap Weights w_mkt"] --> ReverseOpt["Reverse Optimization:\nΠ = λ Σ w_mkt"]
        Sigma["Covariance Matrix Σ"] --> ReverseOpt
        Lambda["Risk Aversion λ = (E[R_m] - r_f) / σ_m^2"] --> ReverseOpt
        ReverseOpt --> Prior["Prior Return Distribution:\nN(Π, τ Σ)"]
    end

    subgraph Subjective_Views ["2. Subjective Investor Views"]
        P_mat["Pick Matrix P (Absolute / Relative)"]
        Q_vec["View Returns Vector Q"]
        Omega["View Uncertainty Matrix Ω (Diagonal / User Confidence)"]
        P_mat & Q_vec & Omega --> ViewDist["Views Distribution:\nP E[R] ~ N(Q, Ω)"]
    end

    subgraph Bayesian_Blending ["3. Bayesian Master Updating"]
        Prior & ViewDist --> BL_Engine["Black-Litterman Formula:\nμ_BL = [(τΣ)^-1 + P^T Ω^-1 P]^-1 [(τΣ)^-1 Π + P^T Ω^-1 Q]"]
        BL_Engine --> PostDist["Posterior Distribution: N(μ_BL, Σ_BL)"]
    end

    subgraph Portfolio_Execution ["4. Constrained Optimization"]
        PostDist --> CLA["Critical Line Algorithm (CLA) / Quadratic Solver"]
        CLA --> OptWeights["Optimal Robust Asset Allocation w*"]
    end
```

### 3. Kahneman-Tversky Prospect Theory: Value & Weighting Architecture

```mermaid
flowchart LR
    subgraph Decision_Phases ["Two-Phase Decision Process"]
        Raw["Risky Prospects"] --> Edit["1. Editing Phase:\nCoding (Ref Point), Combination, Segregation, Cancellation, Simplification"]
        Edit --> Eval["2. Evaluation Phase:\nV = Σ w(p_i) * v(x_i)"]
    end

    subgraph Asymmetric_Value ["S-Shaped Value Function v(x)"]
        Eval --> Gains["Gains (x ≥ 0): Concave / Risk-Averse\nv(x) = x^α  (α ≈ 0.88)"]
        Eval --> RefPoint["Reference Point (Status Quo / Wealth Level)"]
        Eval --> Losses["Losses (x < 0): Convex / Risk-Seeking\nv(x) = -λ (-x)^β  (λ ≈ 2.25 Loss Aversion)"]
    end

    subgraph Probability_Weighting ["Inverse S-Curve Weighting w(p)"]
        Eval --> Overweight["Overweights Rare Tail Events (p → 0)\nLottery Preferences & Disaster Insurance"]
        Eval --> Underweight["Underweights Moderate & High Probabilities (p → 1)"]
    end
```

### 4. Behavioral Portfolio Theory (BPT) Layered Pyramid vs MVO

```mermaid
flowchart TD
    subgraph BPT_Pyramid ["Behavioral Portfolio Theory (BPT-MA) Layered Structure"]
        TopLayer["Top Layer: Aspirational Wealth / Speculation\nHigh Risk / High Return (Growth Stocks, Options, Crypto)\nGoal: Chance of Becoming Wealthy (Risk-Seeking)"]
        MidLayer["Middle Layer: Capital Preservation & Moderate Growth\nModerate Risk / Balanced Yield (Blue-Chips, Corporate Bonds)\nGoal: Maintain Standard of Living"]
        BaseLayer["Base Layer: Downside Protection & Safety\nLow Risk / High Liquidity (Cash, T-Bills, Treasury Bonds)\nGoal: Protection from Poverty / Loss Avoidance"]
        
        TopLayer --- MidLayer --- BaseLayer
    end

    subgraph Traditional_MVO ["Traditional MVO Framework"]
        Unified["Single Mean-Variance Optimization Pool\nEntire Wealth Evaluated Globally via Covariance Matrix Σ\nTreats All Dollars as Fungible"]
    end
```

### 5. Behaviorally Modified Asset Allocation (BMAA) Decision Matrix

```mermaid
flowchart TD
    Client["Client Diagnostic Assessment"] --> Wealth["Evaluate Relative Wealth &\nStandard of Living Risk (SLR)"]
    Client --> Biases["Identify Dominant Behavioral Biases:\nCognitive vs Emotional"]

    Wealth & Biases --> Matrix{"BMAA Allocation Matrix"}

    Matrix -->|"Low SLR (High Wealth) + Cognitive"| Q1["Moderate / Educate:\nAllocation close to MPT / Efficient Frontier"]
    Matrix -->|"Low SLR (High Wealth) + Emotional"| Q2["Adapt / Accommodate:\nAllow customized deviation from MPT to satisfy emotional comfort"]
    Matrix -->|"High SLR (Low Wealth) + Cognitive"| Q3["Moderate / Educate:\nStrictly steer client toward MPT to protect lifestyle"]
    Matrix -->|"High SLR (Low Wealth) + Emotional"| Q4["Moderate with Compromise:\nPrimarily enforce MPT, concede minor non-critical adjustments"]
```

### 6. Growth vs. Risk Parity Allocation Paradigm (Module 5)

```mermaid
flowchart TD
    subgraph Growth_Kelly ["1. Kelly Optimal Growth Paradigm"]
        LogU["Log Utility Maximization:\nmax E[ln(1 + f^T R)]"] --> FullKelly["Continuous Full Kelly:\nf* = Σ^-1 (μ - r 1)"]
        FullKelly --> FracKelly["Fractional Kelly (Half-Kelly):\nf = c * f* (c = 0.5)\n75% Growth, 75% Variance Reduction"]
    end

    subgraph Risk_Parity ["2. Risk Parity & Equal Risk Contribution (ERC)"]
        Euler["Euler Variance Decomposition:\nσ_p = Σ w_i MRC_i"] --> ERC_Cond["Equal Risk Condition:\nRC_i = w_i (Σw)_i / σ_p = σ_p / N"]
        ERC_Cond --> Conic["Second-Order Conic Programming (SOCP):\nRelaxed Risk Parity (Gambeta & Kwon)"]
    end

    subgraph ML_Clustering ["3. Unsupervised Clustering Allocation"]
        DistMat["Distance Matrix D_ij = sqrt((1 - ρ_ij)/2)"] --> Medoid["Partitional k-Medoids / PAM Clustering"]
        Medoid --> PPA["Performance Proportional Allocation (PPA)\nRoulette Wheel Selection (Duarte & de Castro)"]
    end
```

### 7. The August 2007 Quant Meltdown Liquidity & Deleveraging Cascade (Module 6)

```mermaid
flowchart TD
    subgraph Catalyst ["1. Exogenous Subprime Shock"]
        Subprime["Subprime Mortgage Portfolio Losses in Multi-Strategy Funds"] --> Margin["Brokers Issue Urgent Margin Calls"]
    end

    subgraph FireSale ["2. Multi-Factor Fire Sale Liquidation"]
        Margin --> Liquidate["Forced Liquidation of Liquid Equity Market-Neutral Portfolios\n(Statistical Arbitrage, Value, Momentum, Reversal)"]
        Liquidate --> PriceImpact["Extreme Adverse Price Impact:\nLongs Sold at Bid, Shorts Covered at Ask"]
    end

    subgraph Contagion ["3. Cross-Fund Contagion & Spread Collapse"]
        PriceImpact --> FactorLoss["Factor Spread Collapses (Long - Short < 0)\nEquity Market-Neutral Portfolios Drop Despite Zero Beta (β = 0)"]
        FactorLoss --> Deleveraging["Other Levered Quant Funds Hit Stop-Losses & Drawdown Limits\nCascading Forced Deleveraging Spiral"]
    end

    subgraph MarketMaker ["4. Market Maker Liquidity Collapse"]
        Deleveraging --> MM_Loss["Market Makers (Contrarian Proxy) Suffer Heavy Losses"]
        MM_Loss --> SpreadBlowout["Market Makers Withdraw Quotes & Widen Spreads (4x-10x)\nComplete Liquidity Evaporation"]
        SpreadBlowout --> SharpRebound["Post-Unwind Sharp Mean-Reversion Rebound (Aug 10-13)"]
    end
```

### 8. End-to-End Machine Learning & Automatic Factor Construction Architecture (Module 6)

```mermaid
flowchart TD
    subgraph Raw_Features ["1. Multi-Source Raw Features"]
        F1["Price Trends (Momentum, Short-Term Reversal)"]
        F2["Liquidity & Volatility Measures (Bid-Ask, Volume, IdioVol)"]
        F3["Fundamental & Accounting Ratios (Size, B/M, Profitability)"]
        F4["Macroeconomic Conditioning (Term Spread, Default Spread, VIX)"]
    end

    subgraph Gu_Kelly_Xiu_ML ["2. Gu-Kelly-Xiu Machine Learning Asset Pricing"]
        Raw_Features --> Huber["Huber Robust Loss Function ρ_δ(e)\nDownweight Outliers"]
        Huber --> Models["Model Family: ElasticNet, GBRT/XGBoost, Shallow NNs (NN1-NN3)"]
        Models --> Interacting["Capture Complex Non-Linear Interactions\n(Momentum x Liquidity x Size)"]
    end

    subgraph Genetic_NNAFC ["3. Automatic Factor Construction (Fang et al. 2020)"]
        Interacting --> Pretrain["Pre-Training via Knowledge Distillation / Model Stealing:\nNeural Net Learns Technical Priors (MA, EMA, MACD) ≥85% Acc"]
        Pretrain --> DiffGP["Tree-Based Genetic Programming (RPN)\nwith Differentiable Soft-Rank Kernels"]
        DiffGP --> Ortho["Orthogonality & Diversity Objective Regularization:\nPenalize Collinear Factor Bloat"]
    end

    subgraph Alpha_Execution ["4. Dynamic Factor Execution"]
        Ortho --> FMB["Fama-MacBeth 2-Step Regression & Shanken EIV Correction"]
        FMB --> Strategy["Max Sharpe Multi-Factor Long/Short Quintile Allocation"]
    end
```

### 9. Information Theory & Graph-Based Portfolio Enhancement Pipeline (Module 7)

```mermaid
flowchart TD
    subgraph Data_Inputs ["1. Asset Return Data Matrix X (N x T)"]
        Raw_X["Raw Asset Return Series X"] --> Sample_Cov["Sample Covariance S & Correlation C\nq = T / N"]
    end

    subgraph Covariance_Regularization ["2. Spectral & Shrinkage Denoising"]
        Sample_Cov --> Shrinkage["Ledoit-Wolf / OAS Linear Shrinkage:\nΣ_shrunk = (1 - δ) S + δ F"]
        Sample_Cov --> RMT_Filter["Marcenko-Pastur Spectral Filter (RMT):\nλ_+ = σ^2 (1 + sqrt(1/q))^2"]
        RMT_Filter --> CREM["Constant Residual Eigenvalue Method (CREM):\nReplace Noise Modes λ_k ≤ λ_+ with Mean"]
        CREM --> Detoning["De-Toning Market Mode Removal:\nC_detoned = C_denoised - λ_1 v_1 v_1^T"]
    end

    subgraph Info_Geometry ["3. Information-Theoretic Distance Metrics"]
        Detoning --> VI_Metric["Variation of Information (VI) Metric:\nVI(X,Y) = H(X,Y) - I(X;Y) = H(X|Y) + H(Y|X)"]
        VI_Metric --> Dist_Mat["Bounded Distance Matrix D_VI ∈ [0, 1]"]
        Dist_Mat --> MST["Minimum Spanning Tree (MST)\nvia Kruskal's Algorithm"]
    end

    subgraph Tree_Allocation ["4. Hierarchical Risk Parity (HRP)"]
        Dist_Mat --> Tree_Cluster["Hierarchical Agglomerative Clustering\nOptimal Number of Clusters (ONC)"]
        Tree_Cluster --> Seriation["Quasi-Diagonalization (Seriation)\nSort Covariance Matrix along Leaves"]
        Seriation --> Rec_Bisect["Recursive Bisection Inverse-Variance Allocation:\nα = V_2 / (V_1 + V_2)  (Zero Matrix Inversion)"]
        Rec_Bisect --> Robust_Weights["Optimal Machine Learning Allocation w*"]
    end
```

### 10. Hierarchical Risk Parity (HRP) 3-Stage Workflow (Module 7)

```mermaid
flowchart LR
    subgraph Stage1 ["Stage 1: Tree Clustering"]
        Corr["Correlation Matrix C"] --> Dist["Angular Distance:\nd_ij = sqrt((1 - ρ_ij)/2)"]
        Dist --> Linkage["Ward's Agglomerative Linkage\n& Dendrogram Tree T"]
    end

    subgraph Stage2 ["Stage 2: Quasi-Diagonalization"]
        Linkage --> Seriation["Recursive Tree Leaf Traversal\nReorder Rows & Columns of Σ"]
        Seriation --> QuasiDiag["Quasi-Diagonalized Covariance Σ*"]
    end

    subgraph Stage3 ["Stage 3: Recursive Bisection"]
        QuasiDiag --> Bisect["Split Cluster C into C_1 and C_2"]
        Bisect --> ClusterVar["Calculate Cluster Variances:\nV_1 = w_1^T Σ_1 w_1,  V_2 = w_2^T Σ_2 w_2"]
        ClusterVar --> AlphaSplit["Optimal Split Factor:\nα = V_2 / (V_1 + V_2)"]
        AlphaSplit --> FinalAlloc["Final Allocations w* (No Inversion)"]
    end
```

### 11. Combinatorial Purged Cross-Validation (CPCV) Path Engine (Module 8)

```mermaid
flowchart TD
    subgraph Combinatorial_Splitting ["1. Combinatorial Splitting: C(N, k) Groups"]
        Data["Complete Historical Dataset T"] --> Folds["Partition into N Folds (e.g. N=6)"]
        Folds --> Combs["Generate C(6, 2) = 15 Unique Train/Test Splits\n(Each test group size = 2 folds)"]
    end

    subgraph Leakage_Control ["2. Information Leakage Prevention"]
        Combs --> Purge["Purging Window:\nDrop train samples whose label lookahead overlaps test interval"]
        Purge --> Embargo["Embargo Window:\nDrop train samples immediately following test set (AR memory)"]
    end

    subgraph Path_Generation ["3. Multi-Scenario Backtest Distribution"]
        Embargo --> Reconstruct["Reconstruct φ = (k/N) * C(N,k) = (2/6)*15 = 5 Continuous Paths"]
        Reconstruct --> SR_Dist["Compute Empirical Distribution of Sharpe Ratios\n(Avoid Single-Path Overfitting)"]
        SR_Dist --> DSR_Eval["Apply Deflated Sharpe Ratio (DSR) Significance Hurdle"]
    end
```

### 12. FinRL Deep Reinforcement Learning Continuous Execution Loop (Module 8)

```mermaid
flowchart LR
    subgraph Env ["Market Environment (Gym / FinRL)"]
        Prices["Market Data & Order Book"] --> Features["Feature Engineering:\nMACD, RSI, CCI, ADX, Turbulence Index"]
        Features --> State["State s_t = [Prices, Tech Indicators, w_{t-1}]"]
    end

    subgraph DRL_Agent ["Continuous Control DRL Agent"]
        State --> Actor["Policy Actor Network π_θ(a|s)\n(Softmax Allocation Head)"]
        Actor --> Action["Action a_t = Portfolio Weights w_t ∈ Δ^{N-1}"]
        Action --> Execution["Execute Rebalancing Trades\nw_t - w_{t-1}"]
    end

    subgraph Feedback_Loop ["Reward & Critic Optimization"]
        Execution --> PnL["Realized Return w_t^T R_t"]
        PnL --> Reward["Reward r_t = Return - (λ/2) Variance - Friction ||Δw||_1"]
        Reward --> Critic["Twin Critic Networks Q_φ1, Q_φ2 (TD3/SAC) / Clipped PPO"]
        Critic --> Update["Update Policy via Policy Gradient:\n∇_θ J(θ) = E[∇_θ ln π_θ(a|s) A^π(s,a)]"]
        Update --> Actor
    end
```

---

## 📖 Sub-Module & Detailed File Breakdown

### [Module 1: Modern Portfolio Theory (MPT) & Markowitz Optimization](./M1)
- **Lessons & Lecture Slides**:
  - [`M1/L1.pdf`](./M1/L1.pdf): Expected returns vector $\boldsymbol{\mu}$, covariance matrix $\mathbf{\Sigma}$, portfolio variance $\sigma_p^2 = \mathbf{w}^T \mathbf{\Sigma} \mathbf{w}$, and the diversification effect across uncorrelated/negatively correlated assets.
  - [`M1/L2.pdf`](./M1/L2.pdf): Markowitz quadratic optimization formulation, Lagrangian multipliers, derivation of the analytical minimum-variance frontier, and the two-fund separation theorem:
    $$\min_{\mathbf{w}} \frac{1}{2} \mathbf{w}^T \mathbf{\Sigma} \mathbf{w} \quad \text{s.t.} \quad \mathbf{w}^T \boldsymbol{\mu} = \mu_0, \quad \mathbf{w}^T \mathbf{1} = 1$$
  - [`M1/L3.pdf`](./M1/L3.pdf): Risk-free borrowing/lending ($r_f$), Capital Allocation Line (CAL), and analytical derivation of the Tangency (Maximum Sharpe Ratio) portfolio:
    $$\max_{\mathbf{w}} \frac{\mathbf{w}^T \boldsymbol{\mu} - r_f}{\sqrt{\mathbf{w}^T \mathbf{\Sigma} \mathbf{w}}} \implies \mathbf{w}^{\star} \propto \mathbf{\Sigma}^{-1} (\boldsymbol{\mu} - r_f \mathbf{1})$$
  - [`M1/L4.pdf`](./M1/L4.pdf): Sensitivity of Markowitz weights to sample estimation error ("error maximization" of mean returns), introducing short-sale constraints ($\mathbf{w} \ge 0$), and shrinkage covariance estimation.

---

### [Module 2: Asset Pricing Models & Factor Investing](./M2)
- **Lessons & Research Papers**:
  - [`M2/L1.pdf`](./M2/L1.pdf): Capital Asset Pricing Model (CAPM) market equilibrium, Capital Market Line (CML), Security Market Line (SML), and market beta:
    $$\beta_i = \frac{\text{Cov}(R_i, R_m)}{\text{Var}(R_m)}, \quad E[R_i] = r_f + \beta_i \left(E[R_m] - r_f\right)$$
  - [`M2/L2.pdf`](./M2/L2.pdf): Total risk decomposition into systematic market risk and idiosyncratic (diversifiable) residual variance:
    $$\sigma_i^2 = \beta_i^2 \sigma_m^2 + \sigma_{\epsilon, i}^2, \quad \text{Jensen's Alpha: } \alpha_i = R_i - \left[r_f + \beta_i(R_m - r_f)\right]$$
  - [`M2/L3.pdf`](./M2/L3.pdf): Arbitrage Pricing Theory (APT), multi-factor linear pricing models, Fama-French 3-Factor (Market, SMB - Size, HML - Value), and 5-Factor extensions (+ RMW Profitability, + CMA Investment).
  - [`M2/L4.pdf`](./M2/L4.pdf) & [`M2/mathematics-09-01668-v2.pdf`](./M2/mathematics-09-01668-v2.pdf): Mathematical foundation of factor covariance matrix decomposition $\mathbf{\Sigma} = \mathbf{B} \mathbf{\Sigma}_F \mathbf{B}^T + \mathbf{D}$, matrix condition numbers, and noise filtering.

---

### [Module 3: The Black-Litterman Model & Probabilistic Scenarios Optimization](./M3)
- **Lessons, Notes & Required Readings**:
  - [`M3/L1.pdf`](./M3/L1.pdf) & [`M3/L1-note.pdf`](./M3/L1-note.pdf): **The Black-Litterman Model**. Reverse optimization from market capitalization weights $\mathbf{w}_{\text{mkt}}$, equilibrium risk aversion parameter $\lambda = \frac{E[R_m] - r_f}{\sigma_m^2}$, implied excess returns $\boldsymbol{\Pi} = \lambda \mathbf{\Sigma} \mathbf{w}_{\text{mkt}}$, investor view matrix $\mathbf{P} \mathbf{E}[R] = \mathbf{Q} + \boldsymbol{\epsilon}$ with uncertainty $\mathbf{\Omega}$, and the Master Bayesian equations:
    $$\bar{\boldsymbol{\mu}}_{BL} = \left[(\tau \mathbf{\Sigma})^{-1} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{P}\right]^{-1} \left[(\tau \mathbf{\Sigma})^{-1} \boldsymbol{\Pi} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{Q}\right]$$
    $$\bar{\mathbf{\Sigma}}_{BL} = \mathbf{\Sigma} + \left[(\tau \mathbf{\Sigma})^{-1} + \mathbf{P}^T \mathbf{\Omega}^{-1} \mathbf{P}\right]^{-1}$$
  - [`M3/L2-reading.pdf`](./M3/L2-reading.pdf) & [`M3/L2-note.pdf`](./M3/L2-note.pdf): **Critical Line Algorithm (CLA) & Corner Portfolios** (*Bailey & López de Prado, 2013*). Exact quadratic programming solver for inequality and box constraints ($\mathbf{w}_{\min} \le \mathbf{w} \le \mathbf{w}_{\max}$), tracking transitions across Karush-Kuhn-Tucker (KKT) turning points along the piecewise linear efficient frontier.
  - [`M3/L3.pdf`](./M3/L3.pdf) & [`M3/L3-note.pdf`](./M3/L3-note.pdf): **Uses and Misuses of the Black-Litterman Model** (*Chincarini & Kim, 2013*). Mathematical analysis of 3 critical implementation pitfalls: (1) omitting the equilibrium prior, (2) using historical sample returns as a prior (inducing circularity), and (3) miscalibrating view confidence $\tau$ and $\mathbf{\Omega}$, causing severe quadratic utility loss.
  - [`M3/L4-reading.pdf`](./M3/L4-reading.pdf) & [`M3/L4-note.pdf`](./M3/L4-note.pdf): **Probabilistic Scenario Optimization (PSO)** (*Shadabfar & Cheng, 2020*). Hybrid Monte Carlo simulation using low-discrepancy Quasi-Random numbers (Sobol sequences), lexicographical ordering, and liability-driven probabilistic portfolio constraints for institutional pension funds.

---

### [Module 4: Behavioral Finance & Applications to Portfolio Theory](./M4)
- **Lessons, Notes & Research Papers**:
  - [`M4/L1.pdf`](./M4/L1.pdf): **Foundations of Behavioral Finance**.
    - Transition from Traditional Finance (Rational Economic Man, perfect information, utility maximization) to Behavioral Finance (Bounded Rationality, Herbert Simon's "Satisficing").
    - Friedman-Savage double inflection utility function explaining simultaneous insurance buying (risk aversion) and lottery purchases (risk seeking).
    - Comprehensive taxonomy of behavioral biases:
      - *Cognitive Errors (Belief Perseverance)*: Conservatism, Confirmation, Representativeness, Illusion of Control, Hindsight bias.
      - *Cognitive Errors (Information Processing)*: Anchoring, Mental Accounting, Framing, Availability.
      - *Emotional Biases*: Loss Aversion, Overconfidence, Self-Control, Status Quo, Endowment, Regret Aversion.
  - [`M4/L2.pdf`](./M4/L2.pdf): **Prospect Theory & Behavioral Anomalies**.
    - Formal Prospect Theory (*Kahneman & Tversky, 1979/1992*): Two-stage decision architecture comprising the **Editing Phase** (Coding relative to reference point, Combination, Segregation, Cancellation, Simplification, Dominance detection) and the **Evaluation Phase**.
    - Asymmetric power value function:
      $$v(x) = \begin{cases} x^\alpha & \text{for } x \ge 0 \\ -\lambda (-x)^\beta & \text{for } x < 0 \end{cases} \quad (\alpha = \beta \approx 0.88, \; \lambda \approx 2.25)$$
    - Probability weighting function $w(p) = \frac{p^\gamma}{\left(p^\gamma + (1-p)^\gamma\right)^{1/\gamma}}$: Overweighting low-probability tail events and underweighting moderate/high probabilities.
    - Preference for positive skewness, **Bowman's Paradox** (negative empirical correlation between accounting risk and return in struggling firms), and the **Equity Premium Puzzle** resolved via **Myopic Loss Aversion** (*Benartzi & Thaler*).
  - [`M4/L3.pdf`](./M4/L3.pdf): **Behavioral Portfolio Theory (BPT) & Behaviorally Modified Asset Allocation (BMAA)**.
    - **Behavioral Portfolio Theory (BPT-MA)** (*Shefrin & Statman, 2000*): Portfolio construction as a multi-layered pyramid of mental accounts (safety vs aspirational wealth) without cross-layer covariance integration.
    - **Adaptive Market Hypothesis (AMH)** (*Andrew Lo*): Evolutionary market dynamics replacing strict EMH; market efficiency fluctuates based on ecological competition, behavioral adaptations, and institutional constraints.
    - **Behaviorally Modified Asset Allocation (BMAA)** (*Stephen Brunel, 2006*): 2-dimensional framework combining **Standard of Living Risk (SLR)** (relative wealth vs goals) with **Bias Type** (cognitive vs emotional) to determine whether an advisor should *Moderate/Educate* (steer toward MPT) or *Adapt/Accommodate* (deviate to satisfy emotional comfort and prevent panic selling).
  - [`M4/L4.pdf`](./M4/L4.pdf): **Investor Classification Typologies & Financial Market Anomalies**.
    - **Barnewall Model (1987)**: Active investors (entrepreneurs, risk-tolerant, need control) vs Passive investors (accumulators, inheritance, risk-averse).
    - **Bailard, Biehl, and Kaiser (BB&K 1986) Model**: 2-axis classification (Confidence [Confident vs Anxious] $\times$ Method of Action [Careful vs Impetuous]) yielding 5 personalities: **Individualist**, **Adventurer**, **Celebrity**, **Guardian**, and **Straight Arrow**.
    - **Pompian Behavioral Investor Types (BITs 2006)**: Passive Preserver, Friendly Follower, Independent Individualist, Active Accumulator.
    - Anatomy of market bubbles and crashes (Kindleberger/Minsky 5-stage cycle: Displacement $\to$ Boom $\to$ Euphoria $\to$ Profit-Taking $\to$ Panic) driven by herding, feedback loops, and narrative fallacies.
    - **Montier's "Seven Sins of Fund Management"** (*James Montier, 2005*): Forecasting illusion, illusion of control, closet indexing, management meetings confirmation bias, storytelling over numbers, overtrading, and myopia.
  - [`M4/GWP.pdf`](./M4/GWP.pdf): **Large-Scale Empirical Study: Prospect Theory for Online Financial Trading** (*Liu, Nacher, Ochiai, Martino, & Altshuler, PLoS ONE 2014*).
    - Massive empirical dataset: 28.5 million trades across 81.3k traders over 28 months from an online social trading platform.
    - First large-scale empirical verification of Prospect Theory's **Reflection Effect** and **Loss Aversion** ($\lambda \approx 2.0$) in live financial markets.
    - Demonstrates the **Disposition Effect**: Traders hold losing positions significantly longer than winning positions ($T_{\text{loss}} \gg T_{\text{win}}$) due to convex risk-seeking in the loss domain.
    - Formulates 3 behavioral metrics distinguishing winning from losing traders: Win rate ratio $R_p$, Holding duration ratio $R_d$, Payoff ratio $R_r$.

---

### [Module 5: Kelly and Risk Parity: Optimizing for Growth and Risk](./M5)
- **Lessons, Notes & Required Readings**:
  - [`M5/L1-note.pdf`](./M5/L1-note.pdf) & [`M5/L1-reading.pdf`](./M5/L1-reading.pdf) (*Chawla, 2020*): **The Kelly Criterion and the Optimal Growth Strategy**.
    - Foundations in Information Theory (*Kelly, 1956*): Maximizing expected logarithmic growth rate $G(f) = \mathbb{E}[\ln(1 + f R)]$ of capital over sequential betting periods.
    - Discrete Bernoulli formula: $f^* = \frac{b p - q}{b} = p - \frac{q}{b}$ where $p$ is win probability, $q = 1 - p$, and $b$ is odds payoff.
    - Continuous Gaussian diffusion approximation (*Merton, 1969* / *Breiman, 1961*):
      $$f^* = \frac{\mu - r}{\sigma^2}, \quad g(f) = r + f(\mu - r) - \frac{1}{2} f^2 \sigma^2$$
    - **Fractional Kelly**: Betting a scaled fraction $c \in (0, 1)$ (e.g., Half-Kelly $c = 0.5$). Retains $75\%$ of maximum growth while cutting portfolio variance by $75\%$ and eliminating severe asymptotic drawdown risk.
  - [`M5/L2-note.pdf`](./M5/L2-note.pdf) & [`M5/L2-reading.pdf`](./M5/L2-reading.pdf): **The Kelly Criterion Evolves** (*Carta & Conversano, 2020*; *Peterson, 2018*).
    - Multi-asset unconstrained Kelly formula: $\mathbf{f}^* = \mathbf{\Sigma}^{-1} (\boldsymbol{\mu} - r \mathbf{1})$.
    - Dynamic Portfolio Optimization with rolling lookback windows (e.g., 24-month moving averages for $\boldsymbol{\mu}$ and $\mathbf{\Sigma}$).
    - Monte Carlo strategy assessment metrics: median vs mean terminal wealth, probability of losing $>50\%$ of wealth ($P(W_T < 0.5 W_0)$), and ruin probability across trade horizons ($T = 100, 1000, 10000$).
    - Decoupled Kelly Optimization (*Peterson, 2018*): Introducing explicit downside risk constraints into Kelly growth, transforming the objective into a 4th-order non-linear polynomial in $N$ dimensions solved via Differential Evolution algorithms.
  - [`M5/L3-note.pdf`](./M5/L3-note.pdf) & [`M5/L3-reading.pdf`](./M5/L3-reading.pdf): **Introducing Risk Parity** (*Gambeta & Kwon, 2020*; *Pfrommer, 2021*; *Sato, 2019*).
    - Mathematical definition of Marginal Risk Contribution ($\text{MRC}_i$) and Total Risk Contribution ($\text{RC}_i$):
      $$\text{MRC}_i = \frac{\partial \sigma_p}{\partial w_i} = \frac{(\mathbf{\Sigma} \mathbf{w})_i}{\sigma_p}, \quad \text{RC}_i = w_i \times \text{MRC}_i = \frac{w_i (\mathbf{\Sigma} \mathbf{w})_i}{\sigma_p}$$
    - Euler's homogeneous decomposition condition: $\sum_{i=1}^N \text{RC}_i = \sigma_p$. Equal Risk Contribution (ERC) requires $\text{RC}_i = \text{RC}_j = \frac{\sigma_p}{N}$ for all $i, j$.
    - Bridgewater "All-Weather" rationale: Addressing the equity concentration trap of traditional 60/40 portfolios (where equities account for $>90\%$ of total portfolio risk).
    - **Relaxed Risk Parity (RRP)** (*Gambeta & Kwon, 2020*): Transforming 4th-order non-convex ERC polynomial constraints into **Second-Order Conic Programming (SOCP)** cone constraints with linear objectives, enabling controlled return-maximization tilts governed by relaxation parameter $\rho$.
  - [`M5/L4-note.pdf`](./M5/L4-note.pdf) & [`M5/L4-reading.pdf`](./M5/L4-reading.pdf): **Machine Learning Extensions of Risk Parity** (*Duarte & de Castro, 2020*; *Mario Castro, 2020*).
    - Partitional Clustering Asset Allocation: Partitioning Around Medoids (PAM), $k$-medoids, and CLARA algorithms replacing hierarchical trees to group collinear assets.
    - Covariance matrix condition number $\kappa(\mathbf{\Sigma}) = \frac{\sigma_{\max}}{\sigma_{\min}}$ and matrix inversion fragility.
    - Distance metric transformation: $D_{i,j} = \sqrt{\frac{1 - \rho_{i,j}}{2}}$ populating non-negative distance matrices with zero diagonals.
    - **Performance Proportional Allocation (PPA)**: Evolutionary roulette wheel selection (fitness proportionate selection) applied hierarchically at inter-cluster and intra-cluster levels.

---

### [Module 6: Advances and Challenges in Factor Investing](./M6)
- **Lessons, Notes & Required Readings**:
  - [`M6/L1-note.pdf`](./M6/L1-note.pdf) & [`M6/L1-reading.pdf`](./M6/L1-reading.pdf): **Factor Investing: Profitable Anomalies or Anomalous Profits** (*Abasi et al., 2020*; *Coqueret & Guida, 2022*; *Sheppard, 2020*).
    - Transition from CAPM single-index models to Arbitrage Pricing Theory (APT) and multi-factor models.
    - Classification of factor spaces: Macroeconomic (inflation, GDP growth), Fundamental (P/B, P/E, ROE, Momentum), and Statistical/Latent (PCA, Autoencoders).
    - Factor Anomaly Zoo and data-snooping / $p$-hacking: The need for higher statistical hurdles ($t \ge 3.0$, *Harvey, Liu, & Zhu, 2016*) and Bayesianized $p$-values with subjective odds ratios $\text{Odds} = \frac{p}{1-p}$.
    - **Fama-MacBeth 2-Step Cross-Sectional Regression**:
      - *Step 1 (Time-Series)*: Regress each asset $i$'s return on factor returns over time $T$ to estimate factor loadings $\hat{\boldsymbol{\beta}}_i$:
        $$R_{i,t} - R_{f,t} = \alpha_i + \sum_{k=1}^K \beta_{i,k} F_{k,t} + \epsilon_{i,t}$$
      - *Step 2 (Cross-Sectional)*: Regress asset returns across all $N$ assets at each time $t$ on estimated betas $\hat{\boldsymbol{\beta}}_i$ to estimate time-varying risk premia $\hat{\lambda}_{k,t}$:
        $$R_{i,t} - R_{f,t} = \gamma_{0,t} + \sum_{k=1}^K \lambda_{k,t} \hat{\beta}_{i,k} + \eta_{i,t}$$
      - Aggregating time-series averages $\bar{\lambda}_k = \frac{1}{T} \sum_{t=1}^T \hat{\lambda}_{k,t}$ with **Shanken (1992) Errors-in-Variables (EIV)** standard error corrections.
  - [`M6/L2-note.pdf`](./M6/L2-note.pdf) & [`M6/L2-reading.pdf`](./M6/L2-reading.pdf): **Smart Beta, Herding, and Not-So-Smart Beta** (*Krkoska & Schenk-Hoppé, 2019*; *Khandani & Lo, 2007/2011*).
    - Smart Beta indexation (Value, Momentum, Low Volatility, Quality, Size) and capacity constraints.
    - Publication bias and post-publication factor decay ("Why Most Published Research Findings Are False").
    - **The 2007 Quant Meltdown** (*Khandani & Lo, 2007/2011*):
      - Detailed forensic analysis of the August 6–10, 2007 quantitative hedge fund crisis.
      - Mechanism: Multi-strategy hedge funds suffered subprime mortgage losses $\to$ executed emergency liquidations of market-neutral long/short equity books $\to$ simultaneous crowded unwinding across common factors (Value, Momentum, Short-Term Reversal) $\to$ market makers suffered massive losses on contrarian inventory $\to$ bid-ask spreads blew out $\to$ cascading margin calls and forced deleveraging across unaffected quant funds with zero net market beta.
      - Contrarian / daily mean-reversion trading strategy as an empirical proxy for market maker liquidity provision.
  - [`M6/L3-note.pdf`](./M6/L3-note.pdf) & [`M6/L3-reading.pdf`](./M6/L3-reading.pdf): **Factor Models with Machine Learning** (*Gu, Kelly, & Xiu, 2020*; *Coqueret & Guida, 2022*; *Esposito, 2022*).
    - Landmark empirical comparison in asset pricing: OLS, Ridge, Lasso, Elastic Net, Principal Component Regression (PCR), Partial Least Squares (PLS), Generalized Additive Models (GAM), Regression Trees, Random Forests, Gradient Boosted Regression Trees (GBRT/XGBoost), and Deep Neural Networks (NN1 to NN5).
    - **Huber Robust Objective Loss Function**:
      $$\rho_\delta(e_i) = \begin{cases} \frac{1}{2} e_i^2 & \text{for } |e_i| \le \delta \\ \delta |e_i| - \frac{1}{2} \delta^2 & \text{for } |e_i| > \delta \end{cases}$$
      Hybridizing $L_2$ squared loss for small errors with $L_1$ absolute loss for extreme crisis outliers.
    - Empirical discoveries: Shallow Neural Networks (NN1–NN3) with early stopping and $L_1$ weight regularization outperform all linear and tree models; top predictive features are dominated by price trends (Momentum, Short-Term Reversal), Liquidity, Volatility, and their non-linear cross-sectional interactions with firm size and valuation ratios.
  - [`M6/L4-note.pdf`](./M6/L4-note.pdf) & [`M6/L4-reading.pdf`](./M6/L4-reading.pdf): **Advanced Automatic Factor Construction** (*Fang et al., 2020*).
    - Transitioning from manual factor selection to automated factor discovery via Evolutionary Algorithms and Genetic Programming (GP).
    - Tree-based GP syntax trees with primitive operators ($+, -, \times, \div$) and terminals represented in Reverse Polish Notation (RPN).
    - Langdon et al. evolutionary loop: stochastic initial population $\to$ fitness evaluation (Information Coefficient / Sharpe) $\to$ tournament selection $\to$ crossover & mutation.
    - Failure mode of traditional GP: Produces large populations of highly correlated, redundant factors ("factor bloat" / lack of diversity), recreating systemic crowded-trade risks.
    - **Neural Network-based Automatic Factor Construction (NNAFC)** (*Fang et al., 2020*):
      1. *Pre-Training Domain Knowledge*: Neural network pre-trained to imitate expert technical rules (MA, EMA, MACD) to $>85\%$ accuracy via knowledge distillation / model extraction.
      2. *Differentiable Kernel Operators*: Substituting discrete, non-differentiable operators (such as `rank()`) with smooth, differentiable kernel functions (temperature-scaled sigmoid kernels) to enable end-to-end backpropagation.
      3. *Factor Diversity Enforcement*: Explicit objective penalty for cross-factor correlation, guaranteeing discovery of novel, orthogonal alpha factors.

---

### [Module 7: Information Theory and Graphs for Improved Portfolios](./M7)
- **Lessons, Notes & Required Readings**:
  - [`M7/L1-note.pdf`](./M7/L1-note.pdf) & [`M7/L1-reading.pdf`](./M7/L1-reading.pdf): **Shrinking (The Problem Of) The Covariance Matrix** (*Ledoit & Wolf, 2003/2004*; *Chen et al., 2010*; *van Hoecke & Margenot*).
    - High-dimensional sample covariance estimation error when $N \approx T$ or $N > T$.
    - **Linear Shrinkage**: Convex combination $\mathbf{\Sigma}_{\text{shrunk}} = (1 - \delta^\star) \mathbf{S} + \delta^\star \mathbf{F}$ targeting constant correlation matrix $\mathbf{F}_{\text{const}}$ or identity matrix $\mu_v \mathbf{I}$, minimizing expected Frobenius loss.
    - **Rao-Blackwell Theorem & Sufficient Statistics**: Conditional expectation with respect to the sample covariance sufficient statistic under Gaussianity yields the **Rao-Blackwell Ledoit-Wolf (RBLW)** and **Oracle Approximating Shrinkage (OAS)** estimators, provably dominating standard LW in Mean Squared Error (MSE).
    - Robust alternatives: **Minimum Covariance Determinant (MCD)** for outlier resistance and **Graphical Lasso (Glasso)** for $L_1$-penalized sparse precision matrix estimation.
  - [`M7/L2-note.pdf`](./M7/L2-note.pdf) & [`M7/L2-reading.pdf`](./M7/L2-reading.pdf): **The Correlation Matrix Reloaded** (*Pedersen, Babu, & Levine, 2021*; *López de Prado, 2020*).
    - **Enhanced Portfolio Optimization (EPO)** (*Pedersen et al., 2021*): Demonstrates that MVO over-allocates to the smallest Principal Components (PCs) where returns are overestimated and volatilities are underestimated. EPO shrinks correlation toward identity $\mathbf{C}_{\text{EPO}} = (1 - w)\mathbf{C} + w \mathbf{I}$, dampening noise modes while interpolating smoothly between MVO, Equal Volatility weighting, and benchmark tracking.
    - **Random Matrix Theory (RMT) & Marcenko-Pastur Distribution (MPD)**: Analytical noise spectral boundary $\lambda_+ = \sigma^2 (1 + \sqrt{N/T})^2$.
    - **Constant Residual Eigenvalue Method (CREM) Denoising**: Replaces all empirical eigenvalues $\lambda_k \le \lambda_+$ with their trace-preserving arithmetic mean $\bar{\lambda}_{\text{noise}}$, preserving total variance $\text{tr}(\mathbf{C}) = N$.
    - **Market Mode De-Toning**: Extracts the pervasive market beta component $\mathbf{C}_{\text{market}} = \lambda_1 \mathbf{v}_1 \mathbf{v}_1^T$, isolating pure cross-asset idiosyncratic correlation geometry.
  - [`M7/L3-note.pdf`](./M7/L3-note.pdf) & [`M7/L3-reading.pdf`](./M7/L3-reading.pdf): **Information and Distance** (*Guo et al., 2018*; *Marti et al., 2017*; *Libman et al., 2022*; *Zhou, 2013*).
    - Limitations of Pearson linear correlation: Fails to detect non-linear dependencies and violates metric space axioms.
    - Information-Theoretic Metrics: Shannon Entropy $H(X)$, Joint Entropy $H(X, Y)$, Conditional Entropy $H(X|Y)$, and **Kullback-Leibler Divergence (KLD)**.
    - **Jaynes' Maximum Entropy Principle** (most uniform unbiased distribution) and **Minimum Cross-Entropy Principle** (closest distribution to prior subject to moment constraints).
    - **Mutual Information (MI)**: $I(X; Y) = H(X) + H(Y) - H(X, Y)$, quantifying all linear and non-linear shared information.
    - **Variation of Information (VI)**: $VI(X, Y) = H(X|Y) + H(Y|X) = H(X, Y) - I(X; Y)$. Proven to satisfy all 4 metric axioms (non-negativity, symmetry, identity of indiscernibles, triangle inequality).
    - **Financial Networks & Minimum Spanning Trees (MST)**: Applying Kruskal's algorithm on metric distance graphs $\mathbf{D}_{\text{VI}}$ to extract topological market backbones and central sector hubs.
  - [`M7/L4-note.pdf`](./M7/L4-note.pdf) & [`M7/L4-reading.pdf`](./M7/L4-reading.pdf): **Hierarchical Risk Parity (HRP)** (*López de Prado, 2016*; *Jain & Jain, 2019*; *Nanakorn & Palmgren, 2021*).
    - Addresses the fatal "error maximization" of MVO by completely eliminating matrix inversion ($\mathbf{\Sigma}^{-1}$).
    - **The 3-Step HRP Engine**:
      1. *Hierarchical Tree Clustering*: Agglomerative hierarchical clustering with Ward's linkage; Optimal Number of Clusters (ONC) via two-pass silhouette score quality maximization.
      2. *Quasi-Diagonalization (Seriation)*: Recursive tree traversal reordering rows/columns of $\mathbf{\Sigma}$ to concentrate maximal covariances along the main diagonal.
      3. *Recursive Bisection*: Bisects sorted clusters $\mathcal{C}_1$ and $\mathcal{C}_2$, allocating weights via inverse cluster variance ratios $\alpha = \frac{\widetilde{V}_2}{\widetilde{V}_1 + \widetilde{V}_2}$, repeating down to singleton assets.
    - **Hierarchical Equal Weight (HEW)**: Simplified benchmark assigning equal capital splits across dendrogram branches.

---

### [Module 8: Better Backtesting and Reinforcement Learning](./M8)
- **Lessons, Notes & Required Readings**:
  - [`M8/L1-note.pdf`](./M8/L1-note.pdf) & [`M8/L1-reading.pdf`](./M8/L1-reading.pdf): **Backtesting Without Overfitting: Deflating Sharpe and Overcoming Selection Bias** (*López de Prado, 2018/2020*; *Bailey & López de Prado, 2014*; *Moen, 2020*).
    - Pitfalls of naive backtesting and the Multiple Testing Crisis in financial economics.
    - **The Seven Sins of Quantitative Investing**: Survivorship bias, Look-ahead bias, Storytelling, Data mining/snooping, Transaction friction omission, Outlier sensitivity, and Shorting borrow constraints.
    - **Selection Bias under Multiple Testing (SBuMT)**: Quantifying the expected maximum Sharpe ratio under the null hypothesis ($H_0: \text{SR} = 0$) across $N$ strategy trials:
      $$\mathbb{E}\left[\max_{n=1,\dots,N} \{SR_n\}\right] \approx \sqrt{V[SR_n]} \left( (1 - \gamma_{\text{Euler}}) Z^{-1}\left(1 - \frac{1}{N}\right) + \gamma_{\text{Euler}} Z^{-1}\left(1 - \frac{1}{N \cdot e}\right) \right)$$
    - **Probabilistic Sharpe Ratio (PSR)** and **Deflated Sharpe Ratio (DSR)** adjusting for non-normality (skewness $\hat{\gamma}_3$, kurtosis $\hat{\gamma}_4$) and trial inflation $SR_0$:
      $$\text{DSR} = \text{PSR}(SR_0) = Z\left(\frac{(\widehat{SR} - SR_0)\sqrt{T-1}}{\sqrt{1 - \hat{\gamma}_3 \widehat{SR} + \frac{\hat{\gamma}_4 - 1}{4}\widehat{SR}^2}}\right)$$
  - [`M8/L2-note.pdf`](./M8/L2-note.pdf) & [`M8/L2-reading.pdf`](./M8/L2-reading.pdf): **Combinatorial Purged Cross-Validation (CPCV)** (*Berger, 2019*; *Ivanov, 2021*; *López de Prado, 2018*).
    - Limitations of Walk-Forward (WF - single historical path, small early training subsets) and standard K-Fold CV (information leakage, non-sequential test sets).
    - **Combinatorial Purged Cross-Validation (CPCV)**: Partitioning data into $N$ groups and selecting $k$ groups for testing generates $\binom{N}{k}$ unique training/testing splits.
    - Reconstructing $\phi = \frac{k}{N} \binom{N}{k}$ distinct out-of-sample backtest equity paths, generating full empirical distributions of Sharpe ratios, drawdowns, and tail metrics.
    - **Purging**: Eliminating training labels overlapping with test horizon boundaries.
    - **Embargoing**: Discarding training data immediately following test partitions to remove autoregressive serial correlation memory.
  - [`M8/L3-note.pdf`](./M8/L3-note.pdf) & [`M8/L3-reading.pdf`](./M8/L3-reading.pdf): **Reinforcement Learning for Portfolio Management** (*Filos, 2018*; *Necchi, 2020*; *Sutton & Barto, 2020*; *Vogiatzis, 2019*).
    - Mapping portfolio management into a Markov Decision Process (MDP): Agent (Portfolio Manager), Environment (Financial Markets / Order Books), State $\mathbf{s}_t$, Continuous Action $\mathbf{a}_t = \mathbf{w}_t \in \Delta^{N-1}$, Reward $r_t$.
    - **Bellman Expectation & Optimality Equations**: Defining recursive state-value $V^*(s)$ and action-value $Q^*(s, a)$ functions.
    - Exploration vs Exploitation trade-off ($\epsilon$-greedy, entropy-regularized objectives).
    - **Policy Gradient Theorem**: Analytical derivation of gradient $\nabla_\theta J(\theta) = \mathbb{E}[\nabla_\theta \ln \pi_\theta(a|s) Q(s, a)]$.
    - Taxonomy of RL agents: Value-Based (DQN), Policy-Based (VPG, TRPO), Actor-Critic (A2C, A3C, DDPG, TD3, SAC, PPO), Model-Free vs Model-Based.
  - [`M8/L4-note.pdf`](./M8/L4-note.pdf) & [`M8/L4-readin.pdf`](./M8/L4-readin.pdf): **Reinforcement Learning in Real Life** (*Liu et al., 2022 [FinRL]*; *OpenAI Spinning Up*).
    - Modular architecture of the **FinRL** library (`AI4FinanceFoundation/FinRL`) for algorithmic quantitative trading.
    - Pipeline: Market data ingestion $\to$ technical feature engineering (MACD, RSI, CCI, ADX, turbulence index) $\to$ gym environment formulation (`StockPortfolioEnv`) $\to$ DRL agent training $\to$ performance backtesting.
    - Comparison of continuous control actor-critic algorithms:
      - **DDPG**: Deterministic policy gradient with replay buffer.
      - **TD3**: Twin Delayed DDPG mitigating Q-value overestimation bias via clipped double Q-learning $\min(Q_1, Q_2)$, delayed actor updates, and target policy smoothing.
      - **PPO**: Proximal Policy Optimization bounding update divergence via clipped surrogate objective $L^{\text{CLIP}}(\theta)$.
      - **SAC**: Soft Actor-Critic optimizing maximum entropy $\mathbb{E}[r_t + \alpha \mathcal{H}(\pi)]$.
    - Integrating linear and non-linear transaction frictions ($c_{\text{trans}} \|\Delta \mathbf{w}\|_1$) directly into RL rewards to eliminate hyper-trading churn.

---

### [Group Work Projects (GWP1 & GWP2)](./GWP)

#### [GWP1: Factor Models & Robust Regression](./GWP/GWP1)
- **Files & Code Documentation**:
  - [`GWP/GWP1/MScFE 652 PM GWP1 Set F (04.08.26).pdf`](./GWP/GWP1/MScFE%20652%20PM%20GWP1%20Set%20F%20%2804.08.26%29.pdf): Group Work Project 1 problem scenario and tasks.
  - [`GWP/GWP1/MScFE642_PM_GWP_1_Group_16961_Code.ipynb`](./GWP/GWP1/MScFE642_PM_GWP_1_Group_16961_Code.ipynb): Complete Python research notebook implementing rolling 3-factor and 5-factor Fama-French regressions, OLS vs Huber Robust RLM estimation, factor beta stability analysis, and out-of-sample backtesting.
  - [`GWP/GWP1/README.md`](./GWP/GWP1/README.md) & [`GWP/GWP1/key-takeaway.md`](./GWP/GWP1/key-takeaway.md): Technical summaries of GWP1.

#### [GWP2: Machine Learning Portfolio Optimization](./GWP/GWP2)
- **Files & Research Reports**:
  - [`GWP/GWP2/README.md`](./GWP/GWP2/README.md): Master technical summary and empirical report for Group Work Project 2.
  - [`GWP/GWP2/MScFE 652 PM GWP2 Set F (04.08.26).pdf`](./GWP/GWP2/MScFE%20652%20PM%20GWP2%20Set%20F%20%2804.08.26%29.pdf): GWP2 scenario and research specifications across 10 securities (AAPL, GOOG, META, TSLA, BAC, GS, LLY, MRK, WMT, XOM).
  - [`GWP/GWP2/MScFE642_PM_GWP_2_Group_16961_Code.ipynb`](./GWP/GWP2/MScFE642_PM_GWP_2_Group_16961_Code.ipynb): Full research implementation covering:
    - Continuous Unconstrained Kelly vs Constrained Kelly ($w_i \le 20\%$).
    - Out-of-sample performance & tail-risk profiling: Full Kelly, Half-Kelly ($0.5 f^*$), and Double-Kelly ($2.0 f^*$) evaluating cumulative returns, Sharpe ratio, Max Drawdown, and $95\%$ Expected Shortfall (CVaR).
    - K-fold Cross-Validation & Purged Backtesting across 2 years of daily data.
    - Machine learning covariance improvements: Marcenko-Pastur RMT Denoising, Market Mode De-Toning, Ledoit-Wolf Shrinkage, Hierarchical Risk Parity (HRP), and Hierarchical Equal Weight (HEW).
  - [`GWP/GWP2/PM_GWP_2_Report_Group_16961.docx`](./GWP/GWP2/PM_GWP_2_Report_Group_16961.docx): Comprehensive group research report synthesizing empirical findings and risk-adjusted comparisons.

---

## 🔑 Key Takeaways & Quantitative Insights

1. **Markowitz Optimization "Error Maximization"**: Unconstrained sample mean-variance optimization acts as an error amplifier, placing extreme long/short bets on assets with overestimated expected returns or underestimated covariances. Imposing long-only constraints ($\mathbf{w} \ge 0$), shrinkage covariance, or Black-Litterman priors is critical for stability.
2. **Bayesian Black-Litterman Superiority**: Black-Litterman solves the estimation error problem by anchoring portfolio weights around the global market capitalization equilibrium prior ($\boldsymbol{\Pi} = \lambda \mathbf{\Sigma} \mathbf{w}_{\text{mkt}}$), allowing explicit, confidence-weighted tilts only where an investor has unique views.
3. **Exact Constraint Handling via CLA**: When real-world box constraints ($\mathbf{w}_{\min} \le \mathbf{w} \le \mathbf{w}_{\max}$) are introduced, generic quadratic solvers can experience numerical instability. The Critical Line Algorithm (CLA) tracks exact turning points and piecewise linear corner portfolios along the efficient frontier.
4. **Prospect Theory Value & Loss Asymmetry**: Human investors do not maximize absolute terminal wealth under concave von Neumann-Morgenstern utility; they evaluate changes relative to a subjective reference point with an S-shaped value function displaying steep loss aversion ($\lambda \approx 2.25$) and nonlinear probability distortion (overweighting tails).
5. **Mental Accounting & Layered BPT Portfolios**: Rather than maintaining a globally diversified mean-variance portfolio, real-world investors mentally partition assets into distinct hierarchical layers (safety vs aspiration). BPT structures portfolios as goal-based pyramids.
6. **BMAA Dynamic Balancing**: Financial advisors must evaluate a client's Standard of Living Risk (SLR) against their bias type (Cognitive vs Emotional). Cognitive biases should be moderated through education, while emotional biases in wealthy clients should be adapted to in order to ensure long-term strategy adherence.
7. **Empirical Edge in Trading**: As proven in Liu et al. (2014), the primary separator between winning and losing market participants is the systematic elimination of the Disposition Effect—cutting losses immediately while letting profitable positions compound.
8. **Kelly Criterion Growth vs. Downside Volatility Drag**: The Kelly criterion maximizes logarithmic wealth growth ($f^* = \frac{\mu - r}{\sigma^2}$), but full Kelly betting produces extreme drawdown volatility ($>80\%$). Adopting a **Half-Kelly ($c = 0.5$)** allocation captures $75\%$ of maximum continuous growth while reducing portfolio variance by $75\%$, providing an optimal buffer against parameter estimation error.
9. **Risk Parity & Equal Risk Contribution (ERC)**: Traditional 60/40 portfolios concentrate $>90\%$ of total volatility risk in the equity sleeve. Risk parity equalizes each asset's marginal risk contribution ($\text{RC}_i = \frac{\sigma_p}{N}$), and can be enhanced via Second-Order Conic Programming (Relaxed Risk Parity) or Partitional Medoid Clustering (PAM/CLARA with PPA) to improve risk-adjusted yields without matrix inversion fragility.
10. **Two-Stage Cross-Sectional Pricing via Fama-MacBeth**: Identifying true factor risk premia requires separating time-series loadings from cross-sectional pricing. Applying the Shanken (1992) correction accounts for errors-in-variables (EIV) from estimated betas, ensuring robust statistical inference against the "factor zoo" snooping bias ($t \ge 3.0$).
11. **Quant Crowding & Endogenous Liquidity Cascades**: As demonstrated in the August 2007 Quant Meltdown (*Khandani & Lo*), market-neutral strategies sharing identical factor signals (Value, Momentum, Short-term Reversal) can suffer catastrophic drawdowns with zero market beta ($\beta = 0$) when exogenous liquidations trigger cascading deleveraging spirals and market maker liquidity evaporation.
12. **Non-Linear Interactions Dominate Factor Models**: In modern empirical asset pricing (*Gu, Kelly, & Xiu, 2020*), shallow neural networks and gradient boosted trees outperform linear models by capturing non-linear interactions between price trends (momentum/reversal), liquidity, and firm characteristics, especially when regularized with Huber robust loss functions.
13. **Automatic Factor Discovery with Differentiable Kernels**: Naive genetic programming generates redundant, collinear factor bloat. Neural Network-based Automatic Factor Construction (*Fang et al., 2020*) solves this by pre-training neural models on expert technical priors, replacing discrete operators with differentiable soft-rank kernels, and explicitly penalizing factor correlation.
14. **High-Dimensional Covariance Ill-Conditioning & Shrinkage**: When $N$ approaches or exceeds $T$, sample covariance matrices become ill-conditioned or singular. Linear shrinkage toward constant correlation or identity targets (Ledoit-Wolf, OAS) provably bounds condition numbers $\kappa(\mathbf{\Sigma})$ and minimizes expected Frobenius estimation error.
15. **Random Matrix Theory (RMT) Denoising & Market Detoning**: Inverting sample covariance matrices inverts eigenvalues, causing MVO to heavily leverage the smallest, spurious noise eigenvectors ($\lambda_k \to 0$). Marcenko-Pastur Constant Residual Eigenvalue Method (CREM) replaces noise eigenvalues $\le \lambda_+$ with their trace-preserving average, while de-toning extracts the dominant market beta mode to expose clean idiosyncratic correlation structures.
16. **Information-Theoretic Variation of Information (VI) Metric**: Pearson correlation captures only linear co-dependence and violates formal metric axioms. The normalized Variation of Information $\widetilde{VI}(X, Y) = 1 - \frac{I(X; Y)}{H(X, Y)} \in [0, 1]$ defines a rigorous metric distance capturing all non-linear, non-parametric co-dependencies for financial network and cluster modeling.
17. **Hierarchical Tree Clustering & Zero-Inversion HRP Allocation**: Marcos López de Prado's Hierarchical Risk Parity (HRP) overcomes MVO's single-pool instability by organizing assets into an agglomerative tree dendrogram, performing quasi-diagonalization seriation, and allocating capital top-down via recursive bisection inverse-variance splits with **zero matrix inversions**.
18. **Empirical Kelly Tail Risk & Half-Kelly Buffer**: In live empirical backtests (GWP2), Double-Kelly suffers catastrophic ruin (drawdowns $>75\%$) from quadratic variance drag $\frac{1}{2}f^2\sigma^2$, while Half-Kelly ($0.5 f^*$) delivers the highest risk-adjusted Sharpe ratio ($1.64$) and cuts maximum drawdowns by more than half relative to Full Kelly.
19. **Overcoming Multiple Testing Bias via Deflated Sharpe**: Repeated backtest iterations without controlling for trial count $N$ creates severe Selection Bias under Multiple Testing (SBuMT). Applying the Deflated Sharpe Ratio (DSR) establishes an asymptotic extreme value theory threshold $SR_0$, filtering out spurious data-mined strategies and adjusting for return non-normality (skewness and kurtosis).
20. **Combinatorial Purged Cross-Validation (CPCV) Path Generation**: CPCV resolves the single-path limitation of Walk-Forward backtesting by generating $\binom{N}{k}$ combinatorial splits and reconstructing $\phi$ complete out-of-sample paths, while strictly enforcing purging of label lookahead overlap and post-test embargoing against autoregressive memory leakage.
21. **Deep Reinforcement Learning & Continuous Control in FinRL**: DRL formulations model portfolio rebalancing directly as a continuous Markov Decision Process. Proximal Policy Optimization (PPO) and Soft Actor-Critic (SAC) achieve superior risk-adjusted returns by combining non-linear feature representations with explicit transaction friction penalties, avoiding turnover churn.

---

## 🔗 Cross-Module Knowledge Linkages

- **$\to$ [01_financial_market](../01_financial_market/README.md)**: Asset class risk-return profiles, option payoff convexity, market maker mechanics, bid-ask spread dynamics, and structural credit risk feed asset universe constraints.
- **$\to$ [03_stochastic_modelling](../03_stochastic_modelling/README.md)**: Continuous-time jump-diffusion processes, Merton portfolio optimization, and HMM regime-switching models generate dynamic input parameters for tactical allocation.
- **$\to$ [04_financial_econometrics](../04_financial_econometrics/README.md)**: Multivariate GARCH (DCC-GARCH), VAR models, and Fama-MacBeth 2-step panel estimators supply dynamic, time-varying conditional covariance matrices $\mathbf{\Sigma}_t$ and factor risk premia to the Black-Litterman and MVO optimizers.
- **$\to$ [07_machine_learning](../07_machine_learning/README.md)**: Unsupervised clustering (k-medoids, PAM, Hierarchical Risk Parity [HRP], Minimum Spanning Trees [MST]), Information Theory metrics (Mutual Information, Variation of Information), Random Matrix Theory (Marcenko-Pastur spectral denoising), tree-based ensembles (Random Forests, XGBoost), and genetic programming algorithms drive non-parametric asset allocation and automated alpha factor construction.
- **$\to$ [08_deep_learning](../08_deep_learning/README.md)**: Deep Neural Networks (NN1–NN5), Knowledge Distillation / Model Stealing, differentiable ranking kernels, and Deep Reinforcement Learning (PPO, DDPG) optimize multi-period dynamic asset allocation subject to downside CVaR and drawdown constraints.
- **$\to$ [09_risk_management](../09_risk_management/README.md)**: Systemic risk network modeling (Granger causality, PCA Absorption Ratio), fire sale contagion dynamics, variance swap replication, Carr-Madan log contracts, and Spadafora Order Statistics jump-diffusion filtering directly feed portfolio downside tail risk mitigation and hedging engines.
