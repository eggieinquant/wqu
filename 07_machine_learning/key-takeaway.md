# Machine Learning in Finance — Key Pedagogical Takeaways
## MScFE 650 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: Standard K-Fold CV & The Data Leakage Illusion
Consider evaluating a daily stock return model using 5-day forward rolling target labels $y_t = \frac{P_{t+5} - P_t}{P_t}$:
- **Standard Random K-Fold CV**: Shuffles observations randomly into 5 train/test splits.
- **Mechanical Failure Mode (Catastrophic Overfitting via Leakage)**:
  Training Fold 1 contains observation $t=100$ (predicting return from day $100 \to 105$). Testing Fold 1 contains observation $t=102$ (predicting return from day $102 \to 107$).
  Because historical price ranges overlap ($102 \to 105$ is shared in both sets), the model simply memorizes future prices. The backtest cross-validation accuracy reaches an unrealistically high $85\%$, but collapses to $48\%$ (random guessing) when deployed in live trading.
- **Solution (Lopez de Prado's Framework)**:
  Apply **Purging** (dropping training labels whose event horizons overlap with the test set) and **Embargoing** (discarding training samples immediately after the test set to eliminate serial memory leakage).

---

### Toy Example 2: OLS Multicollinearity vs. Lasso ($L_1$) Noise Filtering
Consider predicting asset returns using 100 correlated technical indicators ($p = 100, N = 150$):
- **OLS Regression Failure**: $(\mathbf{X}^T \mathbf{X})$ is ill-conditioned. Matrix inversion explodes noise variance, assigning absurd weights ($w_1 = +450, w_2 = -440$) to collinear inputs.
- **Mechanical Failure Mode**: Severe out-of-sample prediction error due to high estimation variance.
- **Lasso ($L_1$) Solution**:
  Adding penalty $+\lambda \|\boldsymbol{\beta}\|_1$ drives non-informative and redundant indicator weights to **exactly zero**, automatically performing sparse feature selection.

---

### Toy Example 3: Markowitz MVO Matrix Inversion vs. Hierarchical Risk Parity (HRP)
Consider allocating capital across 100 assets:
- **Markowitz MVO Failure**: Requires inverting the $100 \times 100$ sample covariance matrix $\mathbf{\Sigma}^{-1}$. Minor estimation errors in correlations cause massive, unstable portfolio rebalancing.
- **Hierarchical Risk Parity (HRP) Solution**:
  Computes a tree distance metric $d_{ij} = \sqrt{0.5(1 - \rho_{ij})}$, builds a hierarchical cluster tree, quasi-diagonalizes the matrix, and allocates weights using **recursive bisection**. HRP requires **zero matrix inversion**, producing extremely stable asset allocations across regimes.

---

## 2. Core Mathematical Formulations & Evolution

### 1. Regularized Regression Loss Objectives

$$\text{Ridge }(L_2): \quad \min_{\boldsymbol{\beta}} \|\mathbf{y} - \mathbf{X}\boldsymbol{\beta}\|_2^2 + \lambda \|\boldsymbol{\beta}\|_2^2 \implies \hat{\boldsymbol{\beta}}_{\text{Ridge}} = (\mathbf{X}^T \mathbf{X} + \lambda \mathbf{I})^{-1} \mathbf{X}^T \mathbf{y}$$

$$\text{Lasso }(L_1): \quad \min_{\boldsymbol{\beta}} \|\mathbf{y} - \mathbf{X}\boldsymbol{\beta}\|_2^2 + \lambda \|\boldsymbol{\beta}\|_1$$

$$\text{ElasticNet}: \quad \min_{\boldsymbol{\beta}} \|\mathbf{y} - \mathbf{X}\boldsymbol{\beta}\|_2^2 + \lambda_1 \|\boldsymbol{\beta}\|_1 + \lambda_2 \|\boldsymbol{\beta}\|_2^2$$

---

### 2. XGBoost 2nd-Order Taylor Objective Optimization
At step $t$, XGBoost expands loss function $\mathcal{L}^{(t)}$ using 1st gradients $g_i$ and 2nd Hessians $h_i$:

$$\mathcal{L}^{(t)} \approx \sum_{i=1}^N \left[ g_i f_t(\mathbf{x}_i) + \frac{1}{2} h_i f_t^2(\mathbf{x}_i) \right] + \gamma T + \frac{1}{2}\lambda \sum_{j=1}^T w_j^2$$

$$g_i = \frac{\partial l(y_i, \hat{y}^{(t-1)})}{\partial \hat{y}^{(t-1)}}, \quad h_i = \frac{\partial^2 l(y_i, \hat{y}^{(t-1)})}{\partial (\hat{y}^{(t-1)})^2}$$

$$\text{Optimal Leaf Weight:} \quad w_j^* = -\frac{\sum_{i \in I_j} g_i}{\sum_{i \in I_j} h_i + \lambda}$$

$$\text{Split Gain:} \quad \text{Gain} = \frac{1}{2} \left[ \frac{G_L^2}{H_L + \lambda} + \frac{G_R^2}{H_R + \lambda} - \frac{(G_L + G_R)^2}{H_L + H_R + \lambda} \right] - \gamma$$

---

### 3. Credit Risk Scoring: Weight of Evidence & Information Value

$$\text{WoE}_i = \ln\left( \frac{\% \text{Good}_i}{\% \text{Bad}_i} \right), \quad \text{IV} = \sum_{i=1}^B (\% \text{Good}_i - \% \text{Bad}_i) \cdot \text{WoE}_i$$

- $\text{IV} < 0.02$: No predictive power (discard feature).
- $0.10 \le \text{IV} \le 0.50$: Strong predictive power for credit scoring.

---

### 4. SHAP (Shapley Additive exPlanations) Attribution

$$\phi_i(x) = \sum_{S \subseteq F \setminus \{i\}} \frac{|S|! (|F| - |S| - 1)!}{|F|!} \left[ f(S \cup \{i\}) - f(S) \right]$$

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Multi-Model Stacking Ensemble Architecture
Build a Level-1 meta-learner trained on Out-Of-Fold (OOF) prediction matrices from diverse Level-0 base estimators (Ridge, Random Forest, XGBoost, LightGBM) to minimize model variance across market regimes.

```
Level-0 Base Learners:  [ Ridge (L2) ]   [ Random Forest ]   [ XGBoost ]   [ LightGBM ]
                                \               |                 /             /
Out-of-Fold Matrix:                              P_oof ∈ R^{N x 4}
                                                        |
Level-1 Meta-Learner:                   [ Ridge / Logistic Meta-Learner ]
                                                        |
Final Output:                                 Robust Alpha Signal
```

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| ML Algorithm / Paradigm | Loss Function / Optimization | Primary Strengths | Financial Failure Mode | Required Validation |
| :--- | :--- | :--- | :--- | :--- |
| **Lasso ($L_1$) Regression** | MSE $+ \lambda \|\boldsymbol{\beta}\|_1$ | Sparse feature selection; zeroes noise | Fails under strong non-linear interactions | Purged $K$-Fold CV |
| **Ridge ($L_2$) Regression** | MSE $+ \lambda \|\boldsymbol{\beta}\|_2^2$ | Handles correlated collinear features | Retains all non-informative features | Purged $K$-Fold CV |
| **Random Forest** | Bagging tree ensemble | Non-linear features; robust to outliers | Can overfit high-frequency noisy returns | Out-of-Bag (OOB) + Purged CV |
| **XGBoost / LightGBM** | 2nd-order Taylor loss $+ \gamma T$ | State-of-the-art tabular classification | Sensitive to hyperparameter tuning | Nested Purged & Embargoed CV |
| **Hierarchical Risk Parity** | Recursive tree bisection | No matrix inversion; highly stable | Sensitive to distance metric choice | Walk-forward backtest |
| **WoE Scorecard** | Log-loss on binned WoE features | Highly interpretable; regulatory compliant | Loss of information from coarse binning | Out-of-Sample ROC-AUC |
