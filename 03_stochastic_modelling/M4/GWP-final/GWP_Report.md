# MScFE 622 Stochastic Modeling - Group Work Project 1
**Quantitative Finance Group**

## 1. Introduction
This project explores the complexities of option pricing beyond the standard Black-Scholes framework. Recognizing that constant volatility is a poor assumption for real-world markets, we implemented and calibrated two advanced models: **Heston (1993)** for stochastic volatility and **Bates (1996)** for jump-diffusion processes.

Our analysis focuses on capturing the "volatility smile" and "skew" typical of equity indices. Furthermore, we extended our modeling to price path-dependent Asian options using Monte Carlo simulations and examined interest rate dynamics through the **Cox-Ingersoll-Ross (CIR)** model. All computational work was conducted in Python, leveraging robust numerical integration techniques and optimization algorithms.

---

## 2. Modeling Stochastic Volatility: The Heston Approach

### 2.1 Model Dynamics
The Heston model introduces a second source of uncertainty—variance itself. We model the asset price process $S_t$ alongside a variance process $v_t$ that follows a square-root mean-reverting path:
$$ dS_t = \mu S_t dt + \sqrt{v_t} S_t dW_t^1 $$
$$ dv_t = \kappa(\theta - v_t)dt + \sigma \sqrt{v_t} dW_t^2 $$

Here, the correlation $\rho$ between the two Brownian motions is crucial. A negative $\rho$ (leverage effect) implies that market drops are accompanied by volatility spikes, a key feature of equity markets.

### 2.2 Calibration Strategy
To ensure robust parameter estimation, we employed two distinct calibration methods. First, the **Lewis (2001)** Fundamental Transform, known for its numerical stability, was used to minimize the Mean Squared Error (MSE) between model and market prices. We then validated these results using the **Carr-Madan (1999)** Fast Fourier Transform (FFT) approach, which efficiently prices options across the entire strike range.

**Key Findings from Calibration:**
The parameters obtained from both methods were highly consistent, suggesting we found a reliable global minimum.
- **Mean Reversion ($\kappa \approx 2.0$)**: Volatility shocks dissipate relatively quickly.
- **Long-Run Volatility ($\sqrt{\theta} \approx 22.3\%$)**: This effectively anchors the variance process.
- **Correlation ($\rho = -0.50$)**: As expected, the negative correlation confirms the presence of the leverage effect.
- **Feller Condition**: We verified that $2\kappa\theta > \sigma^2$. This is a critical check to ensure the variance process remains strictly positive during simulation.

---

## 3. Pricing Asian Options via Monte Carlo

### 3.1 The Challenge of Path Dependency
We were tasked with pricing an **Arithmetic Asian Call Option**. Unlike European options which depend only on the terminal price, the payoff here relies on the average price over the option's life. This "averaging" destroys the log-normal distribution assumption, making analytical solutions difficult.

### 3.2 Simulation Approach
To address this, we implemented a Monte Carlo simulation engine. Using the calibrated Heston parameters, we simulated 10,000 price paths. We paid particular attention to the discretization of the variance process, employing an **Euler-Maruyama scheme with Reflection** to prevent negative variance values—a common pitfall in naive implementations.

### 3.3 Comparative Analysis
Our pricing results for a 15-day At-The-Money (ATM) Asian Call yielded a fair price of **4.7007**.
Notably, this price is lower than that of a comparable European Call. This result aligns with financial theory: the averaging mechanism smooths out extreme price movements, effectively reducing the volatility of the underlying asset and thus lowering the option's premium.

---

## 4. Addressing Skew: The Bates Jump-Diffusion Model

### 4.1 Capturing "Crash-O-Phobia"
While the Heston model performs well generally, it can struggle to capture the steep "smirk" seen in short-term equity options—the market's fear of sudden crashes. To remedy this, we calibrated the **Bates model**, which adds a jump component to the Heston dynamics.

### 4.2 Interpreting the Jump Parameters
The calibration results were telling. The jump intensity ($\lambda \approx 1.2$) suggests the market prices in slightly more than one significant jump per year. More importantly, the mean jump size ($\mu_J \approx -50\%$) indicates that these jumps are exclusively biased to the downside.
This explicitly models the "Crash-O-Phobia" inherent in the market, explaining why deep out-of-the-money Puts trade at such high premiums.

### 4.3 Practical Application
Finally, we priced a **70-day Put Option** (Strike 95%) for a client using this calibrated model. The fair value was determined to be **25.42**, but we quoted a client price of **26.43**. This spread accounts for the significant hedging difficulty (gamma risk and slippage) associated with jump-diffusion models.

---

## 5. Interest Rate Dynamics: The CIR Model

### 5.1 Why CIR?
For interest rate modeling, we selected the **Cox-Ingersoll-Ross (CIR)** framework over the Vasicek model. The key advantage lies in its square-root diffusion term, which naturally prevents interest rates from becoming negative—a necessary condition for stable long-term modeling in this context.

### 5.2 Simulation Results
The calibrated parameters revealed a very strong mean reversion ($\kappa \approx 4.9$), indicating that interest rate deviations are expected to be short-lived. We simulated 1,000 paths over a one-year horizon, confirming that the rates remained non-negative throughout, validating the model's appropriateness for risk management tasks like CVA calculation.

---

## 6. Conclusion
This project successfully demonstrated the necessity of moving beyond simple models to capture complex market realities. The **Heston model** proved essential for stochastic volatility, while the **Bates model** was required to accurately price the short-term skew. Our use of **Monte Carlo** simulation for Asian options and the **CIR** framework for rates highlighted the importance of choosing the right tool for each financial instrument. Ultimately, the analysis underscores that for equity indices, incorporating leverage effects and crash risk is not optional—it is a requirement for accurate pricing.
