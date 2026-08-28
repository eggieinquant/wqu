---
description: Universal standards for authoring quantitative finance pedagogy, mathematical notation breakdowns, and vector visualizations.
trigger: always_on
---

# Quantitative Pedagogy & Mathematical Documentation Standards

## 1. Pedagogical Architecture for Quantitative Topics
When explaining quantitative concepts or authoring `key-takeaway.md` files, follow the 5-pillar structure:
1. **Intuitive Metaphor**: Clear, accessible real-world analogy (e.g., house equity as a call option, telephone game for RNN vanishing gradients).
2. **🏷️ Notation Breakdown**: Explicitly list all symbols, domains, units, and definitions before calculations.
3. **Step-by-Step Numerical Calculation**: Concrete numbers walking through arithmetic, intermediate transformations, and final metrics.
4. **Calculus & Analytical Derivation**: Formal mathematical proofs, Taylor expansions, and continuous calculus foundations.
5. **Mechanical Failure Modes**: How assumptions break down in extreme market regimes (e.g., liquidity spirals, Feller condition violations, correlation breakdowns).

## 2. Visualization Standards (Strict: No ASCII Art)
- **Prohibited**: Do NOT use monospaced text drawings or ASCII art for quantitative curves, payoff plots, or decision boundaries.
- **Mandatory Vector Line Charts**: Use native Mermaid `xychart-beta` for functional curves, option payoff profiles, and parameter trade-offs.
- **State & Flow Logic**: Use Mermaid `flowchart TD/LR` or `stateDiagram-v2` with clean color styling (`fill:#...`, `stroke:#...`).
- **Tabular Synthesis**: Accompany every chart with a structured economic regime table detailing states, conditions, formulas, and outcomes.

## 3. LaTeX Math & Currency Syntax Safety
- **Plain Text for Currency & Percentages**: Write monetary values (`$100,000`, `$5M`, `$85M`), percentage ranges (`5% – 15%`), and units (`USD Millions`, `USD per share`) as plain text outside LaTeX math mode.
- **Strict LaTeX Delimiters**: Use `$ ... $` or `$$ ... $$` strictly for pure algebraic variables, Greek letters, and mathematical equations.
- **Avoid Syntax Clashes**: Never combine double dollar signs with LaTeX escapes (avoid `$\$` and `($5\% - 15\text{M}$)`).

## 4. Master Notation Glossaries
Every quantitative module must maintain a 4-column Master Glossary table in both `key-takeaway.md` and `README.md`:

| Symbol | Mathematical / Economic Meaning | Typical Units / Range | Context & Core Formula |
| :--- | :--- | :--- | :--- |
| **$V_0, V_t$** | Enterprise Asset Value | USD Millions | Merton Model: $V_0 = E_0 + D_0$ |
