# Deep Learning in Finance — Key Pedagogical Takeaways
## MScFE 690 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: Vanishing Gradients in RNNs vs. The LSTM Constant Error Carousel
Consider predicting monthly volatility using a 100-day historical window of daily returns:
- **Standard Recurrent Neural Network (RNN)**:
  Hidden state update: $\mathbf{h}_t = \tanh(\mathbf{W}_{hh} \mathbf{h}_{t-1} + \mathbf{W}_{xh} \mathbf{x}_t + \mathbf{b})$.
- **Mechanical Failure Mode (Vanishing Gradients)**:
  During Backpropagation Through Time (BPTT), the gradient of loss $\mathcal{L}$ with respect to early state $\mathbf{h}_1$ involves a chain product of Jacobians:

$$\frac{\partial \mathbf{h}_T}{\partial \mathbf{h}_1} = \prod_{k=2}^T \mathbf{W}_{hh}^T \text{diag}\left(1 - \mathbf{h}_k^2\right)$$

  If eigenvalues of $\mathbf{W}_{hh}$ are $< 1$, gradients decay exponentially to zero ($\to 0$) after $15-20$ time steps. Standard RNNs completely forget early market regimes.
- **LSTM Solution**:
  Replaces simple hidden states with a **Cell State $C_t$** driven by additive updates:

$$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$

  Because updates are additive rather than multiplicative, the gradient flows backwards through time without exponential decay (the **Constant Error Carousel**).

---

### Toy Example 2: Gramian Angular Fields (GAF) & 2D Vision Financial Encoding
Consider feeding daily stock return series $X = \{x_1, \dots, x_N\}$ into a computer vision Convolutional Neural Network (CNN):
- **Naive Approach**: Feeding 1D time series directly into 2D ResNet models forces arbitrary reshaping, destroying temporal spatial semantics.
- **GAF Solution**: Map 1D series to polar coordinates $\phi_i = \arccos(\tilde{x}_i)$, then build 2D Gramian matrices:

$$\text{GASF}_{i,j} = \cos(\phi_i + \phi_j) = \tilde{x}_i \tilde{x}_j - \sqrt{1 - \tilde{x}_i^2} \sqrt{1 - \tilde{x}_j^2}$$

$$\text{GADF}_{i,j} = \sin(\phi_i - \phi_j) = \sqrt{1 - \tilde{x}_i^2} \tilde{x}_j - \tilde{x}_i \sqrt{1 - \tilde{x}_j^2}$$

This preserves temporal ordering along the main diagonal and maps quasi-periodic chart patterns into 2D image matrices, allowing deep 2D computer vision CNNs to detect market structure.

---

### Toy Example 3: Deep Reinforcement Learning (DRL) Reward Shaping
Consider training a Proximal Policy Optimization (PPO) agent to manage a multi-asset portfolio:
- **Naive Reward (Raw Cumulative PnL)**: $R_t = \sum r_t$.
- **Mechanical Failure Mode (Tail Risk Exploitation)**:
  The DRL agent learns to exploit high-leverage bets to maximize short-term PnL, resulting in massive left-tail drawdowns ($> -60\%$) during out-of-sample backtests.
- **Differential Sharpe Ratio (DSR) Solution**:
  Shape the reward function to penalize downside variance: $R_t = \text{DSR}_t = \frac{\Delta \mu_t}{\sigma_t} - \frac{\mu_t \Delta \sigma_t^2}{2 \sigma_t^3}$. The policy network learns to optimize risk-adjusted returns while maintaining capital preservation constraints.

---

## 2. Core Mathematical Formulations & Evolution

### 1. Complete LSTM Gating Formulations

$$\text{Forget Gate:} \quad f_t = \sigma(\mathbf{W}_f \mathbf{x}_t + \mathbf{U}_f \mathbf{h}_{t-1} + \mathbf{b}_f)$$

$$\text{Input Gate:} \quad i_t = \sigma(\mathbf{W}_i \mathbf{x}_t + \mathbf{U}_i \mathbf{h}_{t-1} + \mathbf{b}_i)$$

$$\text{Candidate State:} \quad \tilde{C}_t = \tanh(\mathbf{W}_c \mathbf{x}_t + \mathbf{U}_c \mathbf{h}_{t-1} + \mathbf{b}_c)$$

$$\text{Cell State Update:} \quad C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t \quad (\text{Additive Gradient Highway})$$

$$\text{Output Gate:} \quad o_t = \sigma(\mathbf{W}_o \mathbf{x}_t + \mathbf{U}_o \mathbf{h}_{t-1} + \mathbf{b}_o), \quad \mathbf{h}_t = o_t \odot \tanh(C_t)$$

---

### 2. Transformer Scaled Dot-Product & Multi-Head Self-Attention

$$\text{Attention}(\mathbf{Q}, \mathbf{K}, \mathbf{V}) = \text{softmax}\left( \frac{\mathbf{Q} \mathbf{K}^T}{\sqrt{d_k}} \right) \mathbf{V}$$

$$\text{MultiHead}(\mathbf{Q}, \mathbf{K}, \mathbf{V}) = \text{Concat}(\text{head}_1, \dots, \text{head}_h) \mathbf{W}^O, \quad \text{where } \text{head}_i = \text{Attention}(\mathbf{Q}\mathbf{W}_i^Q, \mathbf{K}\mathbf{W}_i^K, \mathbf{V}\mathbf{W}_i^V)$$

---

### 3. PPO Clipped Surrogate Loss (Deep Reinforcement Learning)

$$\mathcal{L}^{\text{CLIP}}(\theta) = \hat{\mathbb{E}}_t \left[ \min\left( r_t(\theta) \hat{A}_t, \; \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon) \hat{A}_t \right) \right]$$

$$\text{where } r_t(\theta) = \frac{\pi_\theta(a_t \mid s_t)}{\pi_{\theta_{\text{old}}}(a_t \mid s_t)}, \quad \hat{A}_t = \text{Generalized Advantage Estimator (GAE)}$$

---

### 4. Variational Autoencoder (VAE) ELBO & Reparameterization Trick

$$\mathcal{L}_{\text{VAE}}(\theta, \phi; \mathbf{x}) = \mathbb{E}_{q_\phi(\mathbf{z} \mid \mathbf{x})}[\ln p_\theta(\mathbf{x} \mid \mathbf{z})] - D_{\text{KL}}\left( q_\phi(\mathbf{z} \mid \mathbf{x}) \,\|\, p(\mathbf{z}) \right)$$

$$\text{Reparameterization Trick:} \quad \mathbf{z} = \boldsymbol{\mu}_\phi(\mathbf{x}) + \boldsymbol{\sigma}_\phi(\mathbf{x}) \odot \boldsymbol{\epsilon}, \quad \boldsymbol{\epsilon} \sim \mathcal{N}(\mathbf{0}, \mathbf{I})$$

This allows backpropagation gradients to flow directly through stochastic latent sampling layers.

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Walk-Forward Expanding-Window Cross Validation
To validate deep neural networks on highly non-stationary asset prices:

```
Train Split 1 [2018 - 2021]  ---> Validate OOS Q1 2022
Train Split 2 [2018 - 2022]  ---> Validate OOS Q1 2023
Train Split 3 [2018 - 2023]  ---> Validate OOS Q1 2024
```
Never evaluate deep financial architectures on fixed static random splits.

### 2. Synthetic Market Generation via TimeGAN
Train TimeGAN architectures combining joint unsupervised adversarial loss with supervised stepwise next-step loss to produce realistic synthetic crisis scenarios for portfolio stress testing.

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Deep Learning Architecture | Core Computational Mechanism | Primary Advantage in Finance | Computational Complexity | Key Failure Mode |
| :--- | :--- | :--- | :--- | :--- |
| **Multi-Layer Perceptron (MLP)** | $\mathbf{a} = \sigma(\mathbf{W}\mathbf{x} + \mathbf{b})$ | Fast baseline tabular model | $\mathcal{O}(N \cdot d)$ | Ignores temporal sequence ordering |
| **LSTM / GRU** | Constant Error Carousel $C_t$ | Captures long-term sequential dependencies | $\mathcal{O}(T \cdot d^2)$ | Information bottleneck over long sequences |
| **CNN-GAF (2D Vision)** | $\text{GASF} / \text{GADF} \to \text{ResNet}$ | Encodes chart spatial structure in 2D | $\mathcal{O}(T^2 \cdot k^2)$ | Loss of original price scale sensitivity |
| **Transformer (MHA)** | $\text{softmax}(\mathbf{Q}\mathbf{K}^T / \sqrt{d_k}) \mathbf{V}$ | Parallel sequence processing; self-attention | $\mathcal{O}(T^2 \cdot d)$ | Requires massive training data to avoid overfitting |
| **PPO DRL Agent** | Actor-Critic Policy Gradient | Dynamic portfolio rebalancing under friction | High (Environment sampling) | Sensitive to reward function shaping |
| **VAE / TimeGAN** | ELBO Loss $+$ Latent Sampling | Generates synthetic market scenarios | High (Generative Minimax) | Mode collapse in latent space |
