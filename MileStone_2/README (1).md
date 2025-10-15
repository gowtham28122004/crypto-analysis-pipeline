# Milestone 2: Crypto Portfolio Analysis and Database Integration

This project, contained within the `Rules_Crypto.ipynb` notebook, demonstrates a complete, end-to-end data science pipeline. It automatically fetches historical data for multiple cryptocurrencies, stores it in a persistent SQLite database, performs a comprehensive portfolio analysis based on several investment strategies, and generates a final report with data visualizations and a data-driven conclusion. Advanced concepts like parallel processing are used to ensure the pipeline is efficient.

## Milestone 2 Work Summary

All tasks for this milestone have been successfully implemented and integrated into a single, cohesive workflow. The key accomplishments are detailed below.

### 1. Portfolio Math Engine
A robust calculation engine was developed to model and evaluate different portfolio strategies based on the rules from the "1st September" slides.

- **Five Investment Rules Implemented:**
  1.  **By Risk Level:** A balanced approach giving higher weight to safer assets like Bitcoin.
  2.  **By Market Capitalization:** Weights are assigned based on the coin's approximate size in the market.
  3.  **By Investment Goal (Safety & Growth):** Two distinct strategies, one prioritizing capital preservation (more BTC) and another focused on aggressive growth (more ETH and Altcoins).
  4.  **Equal Weighting:** A simple strategy that divides investment equally among all assets.
  5.  **Dynamic / Rebalancing:** A simulation was created to demonstrate how a portfolio would be rebalanced back to its target weights after market fluctuations.
- **Weight Constraints:** The logic was updated to strictly enforce the rule that **no single asset's weight can exceed 50%**.
- **Core Calculations:** The engine correctly calculates the portfolio's daily **return** and its overall **risk** (volatility).

### 2. Database for Storing Metrics
A local SQLite database (`crypto_data.db`) was designed to store both the raw data and the final analysis results, ensuring data persistence and integrity.

- **Two New Tables Created:**
  1.  **`portfolio`**: Stores the high-level summary for each investment strategy, including its name, calculated `expected_return`, and `expected_risk`.
  2.  **`portfolio_assets`**: Stores the detailed breakdown of each portfolio, listing all included `currencies` and their `weights`. A `FOREIGN KEY` correctly links this table back to the `portfolio` table.
- **Store and Fetch Logic:** The script successfully **stores** all calculated metrics and weights into these tables. It then **fetches** the data back to verify the operation and present a summary.

### 3. Parallel Execution
To enhance performance, the pipeline leverages parallel processing for computationally intensive tasks.

- **Concurrent Logic:** The script uses Python's `concurrent.futures.ThreadPoolExecutor` to run multiple tasks at the same time.
- **Parallel Rule Testing:** The analysis of all five portfolio strategies is executed **in parallel**, with each rule being processed on a separate thread.
- **Safe Database Writes:** The results from all parallel threads are gathered and then safely written to the database in a single, sequential transaction to prevent data corruption.

### 4. Comparative Analysis and Reporting
The final part of the project produces a comprehensive report comparing the different investment strategies.

- **Portfolio vs. Single Asset Comparison:** The script simulates and compares the growth of a $100 investment in a diversified portfolio against holding a single asset (Bitcoin).
- **Graph Plotting:** Two key visualizations are generated using `matplotlib`:
  1.  A line chart illustrating the **growth over time**.
  2.  A histogram comparing the **volatility** (distribution of daily returns).
- **Data-Driven Insights and Conclusion:** Based on a final summary table using the **Sharpe Ratio** (a measure of risk-adjusted return), the script prints a clear, data-driven conclusion about which strategies performed best.
- **CSV Export:** The script exports the final analysis results into a CSV file named `portfolio_metrics_and_weights.csv` for easy sharing and further analysis.

## How to Run the Project
The entire project is contained within the `Rules_Crypto.ipynb` Jupyter Notebook.

1.  **Prerequisites:**
    -   Python 3.8+
    -   Required libraries: `pandas`, `numpy`, `requests`, `matplotlib`.

2.  **Execution:**
    -   Open the `Rules_Crypto.ipynb` file in Google Colab or a local Jupyter Notebook environment.
    -   Run the cells in order from top to bottom (or use `Runtime -> Restart and run all`).
    -   The notebook will first execute the data pipeline to create/update the `crypto_data.db` file and then proceed with the full analysis and report generation.

## Final Output Files
- **`crypto_data.db`**: The SQLite database containing all raw price data and the final calculated portfolio metrics.
- **`portfolio_metrics_and_weights.csv`**: A CSV report detailing the composition and performance of each portfolio strategy.
- **`portfolio_vs_single_asset_comparison.csv`**: A CSV report with the data used for the comparative growth charts.