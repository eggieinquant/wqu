# Module 4: Stochastic Processes & Black-Scholes

## 🎯 What is this topic about?

**Core Concept**: Mathematical foundations of continuous-time finance and the famous Black-Scholes model.

### Key Ideas:
- **Geometric Brownian Motion (GBM)**: Mathematical model for stock price evolution
- **Markov Property**: Future prices depend only on current state, not history
- **Ito's Lemma**: Fundamental calculus tool for stochastic processes
- **Black-Scholes Model**: Analytical solution for European option pricing
- **Vasicek Model**: Interest rate modeling with mean reversion

### Theory & Context:
This module transitions from discrete models to continuous-time finance:
- **Stochastic Calculus**: Mathematical framework for random processes
- **Risk-Neutral Valuation**: Theoretical foundation for all option pricing
- **Partial Differential Equations**: Black-Scholes PDE and its solutions
- **Interest Rate Modeling**: Beyond constant rates to dynamic term structures

The mathematical journey:
1. **Random Walks** → **Brownian Motion** → **Geometric Brownian Motion**
2. **Discrete Trees** → **Continuous Processes** → **Analytical Solutions**
3. **Single Asset** → **Multiple Assets** → **Interest Rate Derivatives**

## 💻 What is the code about?

### Files Overview:
- **`Lesson 1: Markov's property and GBM.ipynb`**: Foundation of stochastic modeling
- **`Lesson 2: Ito's Lemma and Black-Scholes model.ipynb`**: Core mathematical tools
- **`Lesson 3: Black-Scholes and Monte Carlo Methods.ipynb`**: Analytical vs numerical methods
- **`Lesson 4: Simulating Interest Rates: Vasicek Model.ipynb`**: Interest rate dynamics
- **`TSLA_wqu_data.csv`**: Real market data for empirical validation

### Code Functionality:
1. **GBM Simulation**:
   ```python
   dS = r * S * dt + sigma * S * sqrt(dt) * random_normal()
   ```

2. **Black-Scholes Formula**:
   ```python
   d1 = (log(S/K) + (r + sigma²/2)*T) / (sigma*sqrt(T))
   d2 = d1 - sigma*sqrt(T)
   Call = S*N(d1) - K*exp(-r*T)*N(d2)
   ```

3. **Monte Carlo Implementation**:
   - Generate thousands of price paths
   - Calculate payoffs at expiration
   - Discount back to present value

4. **Vasicek Interest Rate Model**:
   ```python
   dr = a*(b - r)*dt + sigma*sqrt(dt)*random_normal()
   ```

### Technical Implementation:
- **Numerical Integration**: Solving stochastic differential equations
- **Statistical Methods**: Large-scale simulation and analysis
- **Optimization**: Efficient algorithms for complex calculations
- **Validation**: Comparing analytical and numerical results

## 📋 Module Summary

### What You Learn:
- **Mathematical Foundations**: The "why" behind option pricing formulas
- **Analytical Solutions**: When and how to use closed-form formulas
- **Continuous-Time Finance**: Moving beyond discrete models
- **Interest Rate Modeling**: Beyond constant rates to dynamic models

### Key Mathematical Concepts:
1. **Stochastic Processes**: Random evolution of financial variables
2. **Risk-Neutral Measure**: Theoretical framework for pricing
3. **Martingale Theory**: Mathematical foundation of fair pricing
4. **PDE Methods**: Solving the Black-Scholes equation

### Practical Applications:
- **Option Trading**: Understanding theoretical fair values
- **Risk Management**: Greeks calculation and hedging
- **Portfolio Management**: Multi-asset option strategies
- **Interest Rate Products**: Bonds, swaps, and rate derivatives

### Industry Relevance:
- **Quantitative Finance**: Foundation for all modern pricing models
- **Risk Management**: Basel regulations and capital requirements
- **Trading Systems**: Real-time pricing and risk calculations
- **Research**: Academic and industry model development

### Connection to Other Modules:
- **From M2/M3**: Provides theoretical foundation for tree models
- **To M5**: Mathematical tools for empirical analysis
- **To GWP**: Theoretical understanding enhances practical implementation

### Key Insights:
1. **Convergence**: Discrete models converge to continuous solutions
2. **Assumptions**: Understanding model limitations and assumptions
3. **Calibration**: Matching models to market data
4. **Extensions**: How basic models extend to complex derivatives

This module provides the mathematical sophistication needed for advanced quantitative finance roles.