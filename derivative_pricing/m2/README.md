# Module 2: Binomial Models & Monte Carlo Methods

## 🎯 What is this topic about?

**Core Concept**: Introduction to discrete-time option pricing models and simulation methods.

### Key Ideas:
- **Binomial Trees**: Model stock prices with two possible movements (up/down) at each time step
- **American Options**: Options that can be exercised at any time before expiration
- **Dynamic Delta Hedging**: Continuously adjusting portfolio to remain risk-neutral
- **Monte Carlo Methods**: Using random sampling to simulate complex financial scenarios

### Theory & Context:
This module introduces the foundational concepts of option pricing beyond the basic Black-Scholes model. It focuses on:
- **Discrete-time modeling**: Breaking time into small steps to model price evolution
- **Early exercise premium**: Understanding why American options are worth more
- **Risk management**: How traders hedge their positions dynamically
- **Simulation techniques**: When analytical solutions aren't available

## 💻 What is the code about?

### Files Overview:
- **`intro_to_american_options.ipynb`**: Implements American option pricing with early exercise checks
- **`Lesson 2: Dynamic Delta Hedging.ipynb`**: Shows how to hedge option positions over time
- **`Lesson 4: Intro to Monte Carlo Methods.ipynb`**: Demonstrates simulation-based pricing
- **`m2_graded_quiz.ipynb`**: Practical exercises and assessments

### Code Functionality:
1. **Binomial Tree Construction**: Creates price trees with up/down movements
2. **Backward Induction**: Works backwards from expiration to find current option value
3. **Early Exercise Logic**: Compares intrinsic value vs. continuation value
4. **Monte Carlo Simulation**: Generates thousands of random price paths
5. **Delta Hedging**: Calculates and adjusts hedge ratios over time

### Technical Implementation:
- Uses NumPy for efficient array operations
- Implements recursive algorithms for tree traversal
- Applies risk-neutral probability measures
- Handles both European and American-style options

## 📋 Module Summary

### What You Learn:
- **Practical Skills**: How to price options when analytical solutions don't exist
- **Risk Management**: Understanding and implementing hedging strategies
- **Computational Finance**: Using simulation and numerical methods
- **Option Theory**: Deep dive into American vs European option differences

### Key Takeaways:
1. **Flexibility**: Discrete models can handle complex features (early exercise, dividends)
2. **Accuracy**: More time steps generally lead to more accurate pricing
3. **Computational Trade-offs**: Balance between accuracy and computational cost
4. **Real-world Application**: These methods are used extensively in practice

### Prerequisites for Next Module:
- Understanding of binomial tree mechanics
- Familiarity with backward induction
- Basic Monte Carlo concepts
- Risk-neutral valuation principles

This module provides the essential building blocks for more advanced models in Module 3 (Trinomial Trees) and beyond.