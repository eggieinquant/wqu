# Financial Markets & Instruments — Key Pedagogical Takeaways
## MScFE 610 Master Quantitative Synthesis

[← Back to Main README.md](./README.md)

---

## 📖 Table of Contents & Quick Module Links
1. [Core Intuition & Mechanical Failure Modes](#1-core-intuition--mechanical-failure-modes)
   - [Toy Example 1: Merton Structural Credit & Equity as a Call Option](#toy-example-1-merton-structural-credit--equity-as-a-call-option)
   - [Toy Example 2: Securitization Subordination & Correlation Breakdown](#toy-example-2-securitization-subordination--correlation-breakdown)
   - [Toy Example 3: Margin Mechanics & Deleveraging Spirals](#toy-example-3-margin-mechanics--deleveraging-spirals)
2. [Core Mathematical Formulations & Calculus Derivations](#2-core-mathematical-formulations--calculus-derivations)
   - [1. Merton Model Option Partial Derivatives & Greeks](#1-merton-model-option-partial-derivatives--greeks)
   - [2. Continuous Compounding & Limits](#2-continuous-compounding--limits)
   - [3. Modigliani-Miller & WACC Calculus](#3-modigliani-miller--wacc-calculus)
3. [Practical Engineering & Systemic Risk Extensions](#3-practical-engineering--systemic-risk-extensions)
4. [Comparative Synthesis Cheat Sheet](#4-comparative-synthesis-cheat-sheet)

---

<a id="1-core-intuition--mechanical-failure-modes"></a>
## 1. Core Intuition & Mechanical Failure Modes

<a id="toy-example-1-merton-structural-credit--equity-as-a-call-option"></a>
### Toy Example 1: Merton Structural Credit & Equity as a Call Option

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Imagine you buy a house for $\$100,000$ using an $\$80,000$ mortgage debt ($D$) and $\$20,000$ of your own cash equity ($E$). If the house price rises to $\$120,000$, you pay back the bank $\$80,000$ and keep $\$40,000$. But if the house price crashes to $\$50,000$, you can simply walk away, hand the keys to the bank, and lose only your initial cash (equity becomes $\$0$). 
In corporate finance, **company equity is economically identical to a Call Option** written on total company assets $V$ with a strike price equal to nominal debt $D$.

#### 🔢 Step-by-Step Numerical Calculation
- Total Enterprise Firm Value: $V_0 = \$100\text{ Million}$
- Nominal Zero-Coupon Debt Face Value: $D = \$80\text{ Million}$ due in $T = 1\text{ year}$
- Risk-free Rate: $r = 5\%$ ($0.05$)
- Asset Volatility: $\sigma_V = 20\%$ ($0.20$)

**Step 1: Compute $d_1$ and $d_2$**:

$$d_1 = \frac{\ln(V_0 / D) + (r + \frac{1}{2}\sigma_V^2)T}{\sigma_V \sqrt{T}} = \frac{\ln(100 / 80) + (0.05 + 0.5 \times 0.20^2) \times 1}{0.20 \times 1} = \frac{0.22314 + 0.07}{0.20} = \frac{0.29314}{0.20} = 1.4657$$

$$d_2 = d_1 - \sigma_V \sqrt{T} = 1.4657 - 0.20 = 1.2657$$

**Step 2: Lookup Standard Normal Cumulative Distribution Values $\Phi(d)$**:
- $\Phi(d_1) = \Phi(1.4657) \approx 0.9286$
- $\Phi(d_2) = \Phi(1.2657) \approx 0.8972$
- $\Phi(-d_2) = 1 - 0.8972 = 0.1028$ (10.28% risk-neutral default probability)

**Step 3: Compute Equity Value $E_0$ and Corporate Debt Value $D_0$**:

$$E_0 = V_0 \Phi(d_1) - D e^{-rT} \Phi(d_2) = 100 \times 0.9286 - 80 \times e^{-0.05} \times 0.8972 = 92.86 - 80 \times 0.95123 \times 0.8972 = 92.86 - 68.27 = 24.59\text{M}$$

$$D_0 = V_0 - E_0 = 100 - 24.59 = 75.41\text{M}$$

**Step 4: Compute Implied Credit Spread $\mathcal{S}$**:

$$\mathcal{S} = -\frac{1}{T} \ln\left( \frac{D_0}{D e^{-rT}} \right) = -\frac{1}{1} \ln\left( \frac{75.41}{76.098} \right) = -\ln(0.99096) \approx 0.908\% \quad (90.8 \text{ bps})$$

#### 📐 Calculus Derivation & Mechanical Failure Mode (Asset Substitution)
Taking the partial derivative of Equity Value $E_0$ with respect to asset volatility $\sigma_V$ (Vega):

$$\text{Vega}_E = \frac{\partial E_0}{\partial \sigma_V} = V_0 \sqrt{T} \phi(d_1) > 0$$

Because $\text{Vega}_E > 0$ everywhere, equity value increases monotonically with asset volatility $\sigma_V$.
- **Mechanical Failure Mode**: When a firm approaches distress ($V \to D$), shareholders have an incentive to switch firm investments to ultra-volatile, negative-NPV projects. Equity holders capture unlimited upside if the gamble succeeds, while bondholders absorb all downside if it defaults.

---

<a id="toy-example-2-securitization-subordination--correlation-breakdown"></a>
### Toy Example 2: Securitization Subordination & Correlation Breakdown

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Think of credit subordination like a multi-tiered bucket system collecting rainwater (cash flows from a pool of 1,000 mortgages). 
- The **Senior Bucket (AAA)** sits at the top and fills first.
- The **Mezzanine Bucket (BBB)** sits in the middle.
- The **Equity Bucket (First Loss)** sits at the bottom and absorbs leaks/defaults first.

#### 🔢 Step-by-Step Numerical Calculation
- Total Collateral Pool: 1,000 loans of $\$100,000$ each ($100\text{M}$ total).
- Expected Default Rate: $3\%$ per year.
- Tranche Structure:
  - Equity Tranche ($0\% - 5\%$): Absorbs first $\$5\text{M}$ of default losses.
  - Mezzanine Tranche ($5\% - 15\%$): Absorbs losses between $\$5\text{M}$ and $\$15\text{M}$.
  - Senior Tranche ($15\% - 100\%$): Protected against first $\$15\text{M}$ of losses.

**Low Correlation State ($\rho = 0.02$)**:
Default variance across loans is low: $\sigma_{\text{pool}}^2 = N p (1-p) (1 - \rho) \approx 1,000 \times 0.03 \times 0.97 = 29.1$. Expected defaults $= 30$ loans ($\$3\text{M}$).
- Losses ($\$3\text{M}$) are absorbed entirely by the Equity Tranche ($\$5\text{M}$ capacity).
- Senior Tranche suffers $\$0$ loss $\implies$ AAA rating intact.

**Systemic Crash State ($\rho \to 0.85$)**:
During a housing crisis, default correlation spikes. Variance expands: $\sigma_{\text{pool}}^2 \approx N p (1-p) [1 + (N-1)\rho] = 29.1 \times [1 + 999 \times 0.85] = 24,739$.
Defaults cluster violently: 200 loans default ($\$20\text{M}$ loss).
- Equity Tranche ($0-5\%$ / $\$5\text{M}$) wiped out ($100\%$ loss).
- Mezzanine Tranche ($5-15\%$ / $\$10\text{M}$) wiped out ($100\%$ loss).
- Senior Tranche ($15-100\%$) loses $\$5\text{M}$ ($5.88\%$ principal loss) $\implies$ Catastrophic downgrade.

---

<a id="toy-example-3-margin-mechanics--deleveraging-spirals"></a>
### Toy Example 3: Margin Mechanics & Deleveraging Spirals

#### 💡 The Intuitive Metaphor (Easiest to Understand)
Borrowing on margin is like renting a house with a mandatory security deposit. If the property value drops below your collateral limit, the landlord demands immediate cash. If you can't pay, they kick you out and sell your furniture at a liquidation discount.

#### 🔢 Step-by-Step Calculation & Calculus of Margin Call Trigger
- Investor shorts $N = 1,000$ shares at price $P_0 = \$100$.
- Initial Short Value $= \$100,000$. Initial Margin Requirement $= 50\% \implies \$50,000$ collateral cash.
- Total Initial Account Cash Assets $= \$100,000 + \$50,000 = \$150,000$.
- Maintenance Margin ($\text{MM}$) $= 30\%$.

**Deriving the Critical Trigger Price $P^{\star}$**:

$$\text{Margin Ratio}(P) = \frac{\text{Total Account Cash Assets} - N \cdot P}{N \cdot P} = \text{MM}$$

$$150{,}000 - 1{,}000 P^{\star} = 0.30 \times (1{,}000 P^{\star}) \implies 150{,}000 = 1{,}300 P^{\star} \implies P^{\star} = \frac{150{,}000}{1{,}300} = 115.38$$

If stock price rises above $\$115.38$, Account Equity drops below $\$34,615.40$ ($30\%$), triggering an immediate margin call.

---

<a id="2-core-mathematical-formulations--calculus-derivations"></a>
## 2. Core Mathematical Formulations & Calculus Derivations

### 1. Merton Model Option Partial Derivatives & Greeks

$$\text{Equity Delta:} \quad \frac{\partial E_0}{\partial V_0} = \Phi(d_1) \in (0, 1)$$

$$\text{Equity Gamma (Convexity):} \quad \frac{\partial^2 E_0}{\partial V_0^2} = \frac{\phi(d_1)}{V_0 \sigma_V \sqrt{T}} > 0$$

$$\text{Equity Vega:} \quad \frac{\partial E_0}{\partial \sigma_V} = V_0 \sqrt{T} \phi(d_1) > 0$$

---

### 2. Continuous Compounding & Limits
Taking the discrete compounding limit as frequency $m \to \infty$:

$$\text{EAR} = \lim_{m \to \infty} \left(1 + \frac{r}{m}\right)^m - 1 = e^r - 1$$

Continuous discount factor:

$$DF(T) = e^{-rT} = \exp\left( -\int_0^T r(t) dt \right)$$

---

### 3. Modigliani-Miller & WACC Calculus
Weighted Average Cost of Capital with corporate tax shield $T_C$:

$$\text{WACC} = \frac{E}{V} r_E + \frac{D}{V} r_D (1 - T_C)$$

Taking derivative with respect to debt leverage ratio $L = D/V$:

$$\frac{d\text{WACC}}{dL} = \frac{d r_E}{dL} (1-L) - r_E + r_D (1 - T_C)$$

Under Modigliani-Miller Proposition II, $r_E = r_0 + (r_0 - r_D) \frac{D}{E} (1 - T_C)$, ensuring WACC decreases with debt tax shields until financial distress costs dominate.

---

<a id="3-practical-engineering--systemic-risk-extensions"></a>
## 3. Practical Engineering & Systemic Risk Extensions

### Repo Haircuts & Funding Liquidity Shorts
- **Market Liquidity Metric**: Kyle's Lambda $\lambda = \frac{\Delta P}{\text{Volume}}$.
- **Funding Liquidity Metric**: Repo Haircut $h$. Available leverage $= \frac{1}{h}$. A shift in $h$ from $2\%$ to $20\%$ cuts borrowing capacity from $50\times$ to $5\times$, causing systemic margin calls across prime brokers.

---

<a id="4-comparative-synthesis-cheat-sheet"></a>
## 4. Comparative Synthesis Cheat Sheet

| Asset Class / Model | Governing Equation | Primary Risk Driver | Mechanical Failure Mode | Calculus / Derivative Metric |
| :--- | :--- | :--- | :--- | :--- |
| **Merton Structural Credit** | $E_0 = V_0 \Phi(d_1) - D e^{-rT} \Phi(d_2)$ | Firm Volatility $\sigma_V$ | Asset substitution gamble | $\text{Vega}_E = V_0 \sqrt{T} \phi(d_1)$ |
| **Short Position Margin** | $P^{\star} = \frac{\text{Assets}}{(1 + \text{MM}) N}$ | Upside price spikes | Fire-sale deleveraging loop | $\frac{d\text{Margin}}{dP} = -\frac{\text{Assets}}{N P^2}$ |
| **Subordinated Tranche** | $\max(\min(\text{Cash} - L, \text{Attach}), 0)$ | Default correlation $\rho$ | Systemic correlation convergence ($\rho \to 1$) | $\frac{\partial \text{Loss}}{\partial \rho} \gg 0$ in tails |
| **WACC Capital Structure** | $\frac{E}{V} r_E + \frac{D}{V} r_D (1 - T_C)$ | Debt ratio $D/V$ | Insolvency distress costs | $\frac{d\text{WACC}}{d(D/V)}$ |
