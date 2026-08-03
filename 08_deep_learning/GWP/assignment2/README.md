# MScFE 642 Deep Learning for Finance - Group Work Project #2

This repository contains the implementation of **Group Work Project 2**, focusing on the critical risk of **data leakage** and the impact of **validation protocol design** on single-asset trading strategies.

## Project Structure
* **`Group_Work_Project_2.ipynb`**: The executed Jupyter notebook containing the full implementation of Step 1 (single train/test split with leakage) and Step 2 (rolling walk-forward backtesting with leakage).
* **`step2_equity_curves.png`**: The out-of-sample (OOS) equity curves generated from Step 2 walk-forward backtesting.

---

## Executive Summary of Results

A single asset (SPY) log return series was modeled using three deep learning architectures:
1. **Multilayer Perceptron (MLP)**
2. **Long Short-Term Memory (LSTM)**
3. **Convolutional Neural Network with Gramian Angular Fields (CNN-GAF)**

In both Step 1 and Step 2, **intentional information leakage** (`leaky = True`) was introduced: input features at time $t$ include future log returns up to $t+25$ (the forecasting horizon). 

### Performance Comparison Table

| Validation Setup | Model | Out-of-Sample RMSE | Out-of-Sample MAE | Out-of-Sample Directional Accuracy | OOS Backtest Final Equity |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Step 1: Single Split**<br>(Train: 70% / Test: 30%) | MLP <br> LSTM <br> CNN-GAF | 0.1600 <br> 0.0146 <br> 0.0617 | 0.1211 <br> 0.0113 <br> 0.0485 | 55.4% <br> 93.4% <br> 62.9% | 0.9877 <br> 2.0835 <br> 1.6402 |
| **Step 2a: Walk-Forward**<br>(Train: 500 / Test: 500) | MLP <br> LSTM <br> CNN-GAF | 0.2205 <br> 0.0286 <br> 0.0624 | 0.1460 <br> 0.0167 <br> 0.0446 | 60.0% <br> 94.4% <br> 67.5% | 1.9596 <br> 5.1056 <br> 1.8865 |
| **Step 2b: Walk-Forward**<br>(Train: 500 / Test: 100) | MLP <br> LSTM <br> CNN-GAF | 0.2018 <br> 0.0279 <br> 0.0685 | 0.1293 <br> 0.0163 <br> 0.0498 | 58.0% <br> 93.7% <br> 65.2% | 1.9828 <br> 5.0592 <br> 1.5776 |

---

## Discussion & Analysis

### 1. Step 2 Walk-Forward (a & b) vs. Step 1 (Single Split)
* **The Illusion of Rolling Validation Success:** 
  Under the walk-forward validation framework, out-of-sample metrics and backtest equities are significantly higher than the single train/test split. For instance, the LSTM OOS final equity skyrockets from **2.08** in Step 1 to **5.11** in Step 2a and **5.06** in Step 2b.
* **Why Performance Multiplies:**
  Because the features are leaky, the network has access to direct lookahead signals. In walk-forward validation, the model is re-trained periodically (every 500 days in Part a, and every 100 days in Part b). This periodic re-training allows the model's weights to adapt dynamically to the local structure of the leaked information in each fold. Instead of learning a single global representation of the leak, the rolling model continuously calibrates itself to extract the maximum lookahead bias from the most recent window, resulting in highly inflated OOS performance.

### 2. Comparison between Part a (500/500) and Part b (500/100)
* **Re-training Frequency and Model Recency:**
  Part b re-trains the model every 100 observations (8 folds), whereas Part a re-trains every 500 observations (2 folds). 
* **Regime Adaptability & Performance Variations:**
  While frequent re-training (Part b) ensures the model's training data remains adjacent to the test period (offering better error metrics for MLP and LSTM), it also introduces variability. For instance, the CNN-GAF performs better in Part a across all metrics, suggesting that very frequent updates can sometimes introduce noise or instability in architectures with complex spatial features.
* **Regime Adaptability:**
  Financial time series are subject to structural changes and regime shifts. Frequent re-training (Part b) ensures that the training set is always immediately adjacent to the test set, allowing the model to stay closely aligned with the active market regime and local features of the data leak. In Part a, the model trained on days 0-500 is used to predict all the way to day 1000, causing the parameters to become stale and less effective in later days of the fold.

### 3. Backtest Overfitting & Leakage
* **Can Leakage Explain the Results?**
  **Yes, absolutely.** A directional accuracy of **94.4%** (LSTM, Part a) or **93.7%** (LSTM, Part b) on out-of-sample daily returns is impossible in real-world trading markets. These results are entirely artifactual and driven by lookahead bias. The model is simply mapping the future returns (accidentally included in the training features) to the target.
* **Methodological Takeaway:**
  Walk-forward validation is typically considered the gold standard for backtesting financial models because it prevents "overfitting to the future" by strictly respecting temporal order. However, this project demonstrates that **no validation framework can resolve information leakage at the data preparation stage**. If features contain future information, walk-forward validation will not expose the model's failure; instead, it will actually help the model exploit the leak more efficiently, presenting a highly dangerous illusion of out-of-sample profitability.
