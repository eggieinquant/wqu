---
name: quantitative-coursework-authoring
description: Actionable workflow for generating MScFE quantitative finance takeaways, toy examples, Mermaid xychart-beta plots, and notation glossaries.
---

# Quantitative Coursework Authoring Workflow

## When to Use
Use this skill when authoring, updating, or synthesizing quantitative finance coursework, technical documentation, derivative pricing models, econometrics, stochastic calculus, or portfolio management takeaways.

## Step-by-Step Execution Guide

### Step 1: Extract Core Intuition & Mechanical Regimes
- Identify the fundamental economic mechanism (e.g., credit subordination, delta hedging, variance drag, information-time sampling).
- Contrast normal baseline market conditions against crisis failure modes (e.g., correlation spike, liquidity squeeze, vanishing gradients).
- Draft an accessible, relatable real-world metaphor.

### Step 2: Formulate Notation Breakdown & Numerical Walkthrough
- Explicitly list all mathematical variables, parameters, domains, and units under `#### 🏷️ Notation Breakdown:`.
- Construct a concrete numerical scenario with realistic market values (e.g., $100 stock price, 20% volatility, 5% risk-free rate).
- Walk through each arithmetic step and calculation formula explicitly.

### Step 3: Generate Native Mermaid Vector Visualizations
- Plot continuous functional relationships, option payoffs, and parameter trade-offs using Mermaid `xychart-beta`:
```mermaid
xychart-beta
    title "Option Payoff / Metric Curve"
    x-axis "Independent Variable" [x1, x2, x3, x4, x5]
    y-axis "Dependent Metric" min --> max
    line "Series A" [y1, y2, y3, y4, y5]
    line "Series B" [z1, z2, z3, z4, z5]
```
- Accompany the chart with a structured economic regime table.
- Use Mermaid `flowchart TD/LR` or `stateDiagram-v2` with color-coded nodes for balance sheet waterfalls, multi-step NLP pipelines, or Markov regime transitions.

### Step 4: Calculus Proof & Failure Mode Analysis
- Provide rigorous continuous-time calculus derivations (Ito's lemma, Taylor series expansions, PDE solutions, lag polynomial roots).
- Analyze the mechanical breakdown when model assumptions are violated in live trading.

### Step 5: Synchronize Master Notation Glossaries
- Maintain `## 5. Comprehensive Mathematical Notation & Variable Glossary` in `key-takeaway.md`.
- Keep `## 🏷️ Master Quantitative Notation & Variable Glossary` updated in `README.md` with the 4-column standard:
  `| Symbol | Mathematical / Economic Meaning | Typical Units / Range | Context & Core Formula |`
