# Financial Data & Technology — Key Pedagogical Takeaways
## MScFE 650 / 610 Master Quantitative Synthesis

---

## 1. The Core Intuition & Mechanical Failure Modes

### Toy Example 1: Survivorship Bias & The Phantom Sharpe Ratio
Consider testing a quantitative momentum strategy from 2005 to 2025 using the current S&P 500 stock universe list as of 2025.
- **Naive Assumption**: Running the backtest on today's index constituents evaluates valid historical performance.
- **Mechanical Failure Mode (Survivorship Bias)**:
  By selecting stocks that survived until 2025, you implicitly remove all companies that went bankrupt or were delisted during the 2008 financial crisis (e.g., Lehman Brothers, Bear Stearns, Washington Mutual, Enron). The backtest Sharpe ratio is artificially inflated (e.g., from an actual $0.45$ to a phantom $1.85$). When deployed live, the strategy inevitably fails as it encounters uncurated asset universes containing distress risk.

---

### Toy Example 2: Fixed Time-Bar Sampling vs. Information-Based Dollar Bars
Consider sampling market price data to build bar inputs for machine learning models:
- **Fixed Time Bars (1-Minute Intervals)**:
  During low-activity periods (e.g., 12:00 PM - 1:00 PM), 1-minute bars record near-zero volume and random microstructure noise. During market panic events (e.g., 2:00 PM Fed interest rate decision), 1-minute bars condense tens of thousands of trades into a single bar, completely missing micro-regime transitions.
- **Mechanical Failure Mode (Heteroskedasticity & Non-i.i.d. Returns)**:
  Time-sampled returns exhibit heavy fat tails, high autocorrelation in volatility, and non-normal distributions.
- **Dollar Bar Solution**:
  Sampling bars whenever cumulative dollar value traded reaches a fixed threshold $T = \sum p_i v_i$ synchronizes sampling with information arrival. Dollar bar returns approximate an **i.i.d. Gaussian distribution**, restoring valid statistical inference for ML estimators.

---

### Toy Example 3: Unstructured Social Sentiment Noise & Signal Decay
Consider extracting trading signals from $100,000$ raw daily StockTwits/Twitter messages containing ticker tags ($\$AAPL$).
- **Naive Counting**: Buying when raw positive tweet count increases by $50\%$.
- **Mechanical Failure Mode**: Raw message counts are highly non-stationary, dominated by spam bots, and correlated with asset volatility rather than return direction. Naive sentiment indicators decay rapidly and exhibit negative out-of-sample Information Coefficients ($\text{IC} < 0$).

---

## 2. Core Mathematical Formulations & Evolution

### 1. Advanced Intraday Volatility Estimators
Traditional close-to-close sample variance discards intraday price trajectories. Intraday range estimators capture far more statistical information:

$$\text{Parkinson Volatility (High-Low):} \quad \sigma_P = \sqrt{\frac{1}{4 \ln 2 \cdot N} \sum_{i=1}^N \left(\ln \frac{H_i}{L_i}\right)^2}$$

$$\text{Garman-Klass Volatility (OHLC):} \quad \sigma_{GK} = \sqrt{\frac{1}{N} \sum_{i=1}^N \left[ 0.5 \left(\ln \frac{H_i}{L_i}\right)^2 - (2\ln 2 - 1) \left(\ln \frac{C_i}{O_i}\right)^2 \right]}$$

Garman-Klass is up to **$8 \times$ more statistically efficient** than close-to-close variance.

---

### 2. VADER Sentiment Polarity & Compound Score
VADER computes valences across positive ($pos$), negative ($neg$), and neutral ($neu$) lexicon tokens:

$$C = \frac{x}{\sqrt{x^2 + \alpha}} \quad \text{where } x = \sum \text{valence scores}, \; \alpha \approx 15 \quad (C \in [-1, +1])$$

---

### 3. Quantitative Alpha Signal Validation Metrics
To evaluate whether an engineered data feature $S_t$ contains true predictive alpha for forward returns $R_{t+1}$:

$$\text{Information Coefficient (IC):} \quad \text{IC}_t = \text{Corr}(S_t, R_{t+1})$$

$$\text{Rank Information Coefficient:} \quad \text{Rank IC}_t = \text{SpearmanCorr}(S_t, R_{t+1})$$

$$\text{Information Ratio (IR):} \quad \text{IR} = \frac{\mathbb{E}[\text{IC}_t]}{\text{Std}(\text{IC}_t)} \cdot \sqrt{252}$$

A feature with $\text{IC} > 0.03$ and $\text{IR} > 1.5$ is considered a institutional-grade quantitative signal.

---

## 3. Practical Engineering, Stress-Testing & ML Extensions

### 1. Point-In-Time (PIT) Relational Schema Design
To prevent Look-Ahead Bias in financial databases, tables must store explicit historical timestamp indices:
```sql
CREATE TABLE point_in_time_fundamentals (
    ticker VARCHAR(10),
    as_of_date DATE,         -- Period end date (e.g. 2024-12-31)
    filing_date DATE,        -- SEC Public release date (e.g. 2025-02-15)
    metric_name VARCHAR(50),
    metric_value NUMERIC,
    PRIMARY KEY (ticker, filing_date, metric_name)
);
```
Queries must strictly filter `WHERE filing_date <= current_simulation_date`.

### 2. Idempotent Production ETL Engineering
All ETL pipelines must be **idempotent**: re-running an ingestion script over historical data must replace or update records without generating duplicate rows or primary key constraint violations.

---

## 4. Comparative Synthesis & Pedagogical Cheat Sheet

| Data Structure / Resampling Method | Aggregation Criterion | Statistical Properties | Primary Use Case | Critical Failure Mode |
| :--- | :--- | :--- | :--- | :--- |
| **Time Bars** | Fixed Time Interval $\Delta t$ | Non-i.i.d., fat-tailed, heteroskedastic | Standard chart visualization | Undersamples volatility panics |
| **Volume Bars** | Cumulative Volume $V \ge V_{\text{thresh}}$ | Partial variance stabilization | Microstructure order flow analysis | Sensitive to shares outstanding changes |
| **Dollar Bars** | Cumulative Value $\sum p_i v_i \ge T$ | Approximates i.i.d. Gaussian returns | Feature store inputs for ML/DL models | Requires dynamic threshold adjustments |
| **Garman-Klass Volatility** | Intraday OHLC Prices | $8 \times$ efficiency gain over close-to-close | High-frequency volatility trading | Underestimates overnight price jumps |
| **VADER Sentiment** | Rule-Based Lexicon Matching | Normalized Polarity Score $C \in [-1, +1]$ | Social media text sentiment extraction | Blind to financial sarcasm & context |
