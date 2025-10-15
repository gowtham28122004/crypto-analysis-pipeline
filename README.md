# End-to-End Cryptocurrency Data & Analysis Pipeline

This project is a complete, back-end data science pipeline built in Python. It automates the entire workflow of a financial analysis project, from data acquisition to predictive modeling and real-time risk monitoring. The system fetches historical data for multiple cryptocurrencies, stores it in a persistent SQLite database, performs a comprehensive portfolio analysis based on several investment strategies, and trains a predictive LSTM model for price forecasting.

The entire project is designed with professional software engineering practices, including parallel processing for efficiency, secure handling of credentials, and a modular, well-documented codebase.

## 🚀 Key Features

This project demonstrates a full data science and engineering lifecycle, including:

-   **Parallel Data Ingestion:** Fetches historical daily data for 6 major cryptocurrencies (BTC, ETH, SOL, ADA, XRP, DOGE) simultaneously from the free KuCoin API.
-   **Robust Data Storage:** Stores all raw historical data in a local SQLite database (`crypto_data.db`), using `UNIQUE` constraints to ensure data integrity and prevent duplicates.
-   **Advanced Portfolio Analysis:**
    -   Implements and stress-tests **9 distinct portfolio weighting strategies**, including static rules (e.g., `Risk Level`, `Market Cap`) and dynamic, data-driven rules (`Risk-Parity`, `Sharpe-Maximization`, `Momentum`).
    -   Enforces a **40% maximum weight** on any single asset to ensure diversification.
-   **Database for Metrics:** Stores all calculated analysis results (portfolio returns, risk, and asset weights) in dedicated `portfolio` and `portfolio_assets` tables for a permanent, queryable record.
-   **Real-Time Risk Monitoring:**
    -   Implements **6 key risk rules** (Volatility, Sharpe Ratio, Max Drawdown, Sortino Ratio, Beta, and Asset Concentration).
    -   Checks a benchmark portfolio against these rules and stores the PASS/FAIL results in an `risk_assessment` table for auditing.
-   **Automated Alerting:** Automatically sends a detailed **email alert** if any of the monitored risk rules fail.
-   **Predictive Modeling (LSTM):**
    -   Builds and trains a Long Short-Term Memory (LSTM) neural network to predict future cryptocurrency prices.
    -   Achieves a high **R-squared of 0.88** and a low **MAPE of 3.00%**, demonstrating its effectiveness at tracking the price trend.
    -   Saves the trained model to a `.keras` file for future use.
-   **Data Visualization & Reporting:**
    -   Generates plots using `matplotlib` to visually compare the performance of a diversified portfolio against holding single assets.
    -   Exports the final analysis and comparison data to multiple CSV files for easy sharing and further analysis.

## 🛠️ Technologies Used

-   **Programming Language:** Python
-   **Core Libraries:**
    -   `requests`: For making API calls to fetch data.
    -   `sqlite3`: For database creation and interaction.
    -   `pandas` & `numpy`: For data manipulation and numerical calculations.
    -   `concurrent.futures`: For parallel processing (multithreading).
    -   `matplotlib`: For data visualization.
    -   `scikit-learn`: For data scaling and model evaluation.
    -   `tensorflow` / `keras`: For building and training the LSTM predictive model.
    -   `smtplib`: For the automated email alerting system.
-   **Data Storage:** SQLite
-   **Development Environment:** Google Colab / Jupyter Notebook

## 🏃 How to Run the Project

The entire project can be run from a single, unified Python script or Jupyter Notebook.

### Prerequisites

1.  **Python 3.8+**
2.  For email alerts, a **Gmail account** with **2-Step Verification** enabled and a **16-digit App Password**.

### Installation

1.  Clone this repository or download the project files.
2.  Open a terminal in the project directory.
3.  Install the required Python libraries:
    ```bash
    pip install -r requirements.txt
    ```

### Execution

1.  **Configure (for email alerts):** If running in Google Colab, create a secret named `GMAIL_APP_PASSWORD` and store your 16-digit App Password there. Also, update the `SENDER_EMAIL` and `RECEIVER_EMAIL` variables in the script.
2.  **Run the Script:** Execute the main Python script or run the cells of the Jupyter Notebook in order.
    ```bash
    python complete_crypto_pipeline.py
    ```
3.  The script will perform the full end-to-end process: data fetching, database storage, portfolio analysis, risk checking, and predictive modeling. It will display plots on the screen and generate the final database and CSV files in the project directory.

## 📂 Final Output Files

-   **`crypto_data.db`**: The primary SQLite database containing all raw price data and all calculated analysis and risk assessment results.
-   **`lstm_price_predictor.keras`**: The saved, trained LSTM model file, ready to be loaded for future predictions.
-   **`portfolio_metrics_and_weights.csv`**: A CSV report detailing the composition and performance metrics of each portfolio strategy.
-   **`final_performance_report.csv`**: A CSV report containing the time-series data used to plot the cumulative growth of different investment strategies.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.