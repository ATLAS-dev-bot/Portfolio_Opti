# Projects – Portfolio Construction

We aim to develop a set of modular research libraries to systematically investigate several core problems in portfolio construction.  
The order of execution across topics is flexible — progress can be made in parallel, provided that tangible outputs are delivered regularly for each area.


## Consultant Deliverables and Iterative Approach

The consultant is expected to deliver an initial **Version 0 (v0)** of each of the three research topics listed below.

- The **v0 deliverable** should be a functional, well-documented prototype that demonstrates the core logic of the approach (e.g., simplified model, backtest, or simulation).  
- Once v0 is complete for all topics, we will proceed to **refinement iterations**, during which the consultant will:  
  - Enhance model robustness (e.g., include transaction costs, realistic constraints, improved data handling).  
  - Improve code structure, modularity, and integration with existing research libraries.  
  - Expand testing coverage and validation on historical datasets.

This approach ensures continuous progress and early visibility of results across all modules before moving to more advanced refinements.


## General Portfolio Assumptions

Across all research modules, we assume the following characteristics for our portfolios:

- **Market Neutrality:** The portfolio maintains both long and short positions such that overall exposure is cash- or beta-neutral.  
- **Universe:** Assets are individual equities, fully adjusted for corporate actions (splits, dividends, etc.).  
- **Available Data:** Each dataset will include adjusted daily returns, adjusted prices, volumes, average daily volumes (ADVs), and alpha signals.  
- **Alpha Definition:** An *alpha* represents a stock-level predictive signal, typically standardized (e.g., as a z-score) across the universe. Higher values indicate stronger buy signals, while lower values suggest short or sell preferences.


## 1. Optimal Weighting

### Problem Summary
Given a daily alpha signal that is predictive of future returns, the objective is to optimally transform this signal into portfolio weights that best capture its predictive power.

### Research Directions

- **Signal-fitting Approach:**  
  Generate weights by minimizing the distance (e.g., Euclidean or other metrics) between the final portfolio weights and the raw alpha values, under practical constraints such as:
  - Maximum single-stock position (liquidity constraint)  
  - Turnover constraint  
  - Maximum portfolio volatility constraint

- **Expected Return Approach:**  
  Alternatively, estimate expected returns from the alpha signal using filtering or signal-processing techniques, then derive weights using standard optimization frameworks (e.g., mean–variance optimization, risk parity, or optimization under transaction cost constraints).

### References
Grinold & Kahn, Boyd et al., and other quantitative portfolio optimization literature.


## 2. Volatility Targeting

### Problem Summary
Once daily portfolio weights are determined, we aim to apply dynamic leverage to achieve a consistent realized volatility level over time.

### Research Directions

- **Macro (Time-Series) Approach:**  
  Treat the portfolio as a single asset and estimate its volatility from its return history (e.g., using GARCH-type models).  
  The predicted volatility determines the leverage multiplier required to reach the target volatility level.

- **Granular (Cross-Sectional) Approach:**  
  Use the daily stock-level weights and the corresponding covariance matrix to predict portfolio volatility more precisely.  
  The resulting forecast is then used to scale leverage dynamically and maintain the target volatility.

Each method will be backtested to compare the **realized volatility** with the **target volatility**, evaluating stability, return impact, and rebalancing efficiency.


## 3. Optimal Strategy Allocation

### Problem Summary
Given multiple market-neutral strategies — each defined by its own daily portfolio weights — the goal is to derive an optimal allocation into a consolidated master portfolio.

### Research Directions

We will evaluate several allocation methodologies, including:

- **Robust Markowitz Optimization** (assuming expected returns are available)  
- **Risk Budgeting** (equal or constrained risk contribution)  
- **Maximum Diversification** (minimizing correlation concentration)  
- **Black–Litterman Framework** (combining priors with strategy-level views)

Each approach will be benchmarked for robustness, interpretability, and sensitivity to estimation error, using both simulated and historical strategy data.

