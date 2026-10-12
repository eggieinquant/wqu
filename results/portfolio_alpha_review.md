# INSTITUTIONAL MULTI-FACTOR PORTFOLIO AUDIT MEMORANDUM

## 1. Executive Portfolio Verdict: APPROVED WITH SECTOR HEDGE (Conviction: High)
- The proposed target allocation achieves a robust expected CAGR of **+37.9%** and an institutional Sharpe ratio of **3.27**, comfortably beating the WQU benchmark target (Sharpe >= 2.50).
- Capital deployment is efficient at 96.4% deployed across 100-share round lots, with a 3.6% cash buffer reserved for frictional slippage and margin buffer.

## 2. Multi-Factor Alpha Exposure Audit
- **Alpha 18 (VWAP Dislocation Pullback)**: BID (+1.24) and SSB (+1.12) demonstrate extreme transient discounts relative to their 20-day volume-weighted average price. Buying at these dislocation troughs provides an immediate statistical edge.
- **Alpha 2 (Deep Value EV/EBITDA Reversal)**: Both BID and HDB exhibit normalized valuation scores (>0.60), providing a fundamental margin of safety against macro valuation compression.
- **Alpha 9 (Smart Money Volume Accumulation)**: BID shows a massive volume surge ratio (+2.38), indicating institutional accumulation while the price remains stable above local support.

## 3. Sector Concentration & Correlation Risk
- **Primary Risk Exposure**: The portfolio has a **76.3% concentration in Financials/Banking** (BID 30.0%, SSB 23.4%, HDB 22.9%).
- **WQU Independence Constraint Violation**: While WorldQuant theory targets pairwise correlations rho <= 0.25, intra-sector banking correlations on HOSE typically spike to rho >= 0.70 during liquidity shocks.
- **Recommendation**: Cap aggregate banking exposure at 50% by rotating ~25% of active equity into an uncorrelated technology or consumer leader (e.g. FPT at Rank #5 or VNM).

## 4. Vietnam Microstructure & Liquidity Stress Test
- **T+2 Settlement Lock**: If systemic credit news triggers a selloff on Day T, 76% of portfolio equity cannot be sold until Day T+2. Cash buffer of 3.6M VND is adequate for maintenance, but position sizing must not exceed board lot limits.
- **HOSE Floor-Band Boundary Protection**: Dynamic stop-losses at -7.0% (BID: 33,248 VND, VIC: 224,316 VND, SSB: 22,413 VND, HDB: 25,575 VND) match the daily exchange limit floor, effectively shielding against zero-bid limit-down lockouts.
- **Frictional Drag**: Total round-trip frictions (0.15% commission + 0.10% sales tax) total 241,025 VND (~0.24% of capital), well within our 1.5% annual friction budget.

## 5. Actionable Rebalancing & Execution Mandate
1. **Proceed with Execution**: Execute the approved 100-share board lots for BID (800 shs), VIC (100 shs), SSB (900 shs), and HDB (800 shs).
2. **Sector Hedging Adjustment**: On the next rebalancing cycle, introduce a 15-20% allocation to **FPT** (Rank #5, Score +3.10) to neutralize financial sector clustering.
3. **Stop-Loss Execution**: Immediately submit trailing GTC stops at the exact -7.0% floor-band prices.