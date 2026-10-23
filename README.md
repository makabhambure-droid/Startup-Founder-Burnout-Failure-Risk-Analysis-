# Startup Founder Burnout & Failure Risk Analysis (2026)

An end-to-end data analytics project that studies how founder burnout, co-founder conflict, runway and the economic climate relate to startup shutdown risk. It includes a data-cleaning pipeline, exploratory analysis, a predictive model and an interactive risk calculator.

## Dataset

- **File:** `startup_founder_burnout_2026.csv` (final cleaned version)
- **Size:** 50,000 founders x 29 columns, no missing values, no duplicate rows
- **Main columns:**
  - Founder & company: `Founder_Type`, `Founder_Age`, `Industry`, `Funding_Stage`, `Team_Size`, `Economic_Climate`
  - Lifestyle & stress: `Weekly_Work_Hours`, `Sleep_Hours`, `Stress_Score`, `Burnout_Score`, `Work_Life_Balance_Score`
  - Business health: `Runway_Months_Remaining`, `Product_Market_Fit_Score`, `Monthly_Revenue_Growth_Percent`
- **Created columns:**
  - `Shutdown_Probability`: probability (0-1) that the startup shuts down
  - `Shutdown_Risk`: Low (< 0.35), Medium (0.35-0.65), High (> 0.65)
  - `Startup_Failure_Flag`: 1 when `Shutdown_Risk` is High, otherwise 0

## Project description

1. **Cleaning:** missing values, duplicates and wrong data formats were fixed using Python and SQL (VS Code).
2. **Feature engineering:** the three shutdown columns above, plus extra features such as `Sleep_Deficit`, `Stress_Load_Index` and `Recovery_Index`.
3. **EDA:** distributions, correlations, failure rate by segment, statistical tests.
4. **Modelling:** logistic regression and gradient boosting predict `Startup_Failure_Flag` (about 0.95 ROC-AUC in cross-validation). `Shutdown_Probability` and `Shutdown_Risk` are excluded from the inputs to avoid data leakage.
5. **Risk calculator:** a standalone HTML app whose formula is fitted on the dataset (R² = 0.72; AUC = 0.93 for the failure flag).

## Technologies used

Python 3.10+, pandas, NumPy, SQLite (`sqlite3`), Matplotlib, Seaborn, SciPy, scikit-learn, Jupyter Notebook, HTML / Tailwind CSS / Chart.js (calculator).

## Repository contents

| File | Purpose |
|---|---|
| `startup_founder_burnout_analysis.ipynb` | Main notebook (cleaning, features, EDA, model) |
| `startup_founder_burnout_analysis.py` | Same code as a script |
| `startup_failure_risk_calculator.html` | Interactive risk calculator |
| `requirements.txt` | Python dependencies |
| `YourName_ProjectReport.docx` | Full project report |
| `startup_founder_burnout_2026.csv` | Dataset  |

## Setup and run

```bash
# 1. (optional) create a virtual environment
python -m venv venv
venv\Scripts\activate            # Windows
# source venv/bin/activate       # macOS / Linux

# 2. install dependencies
pip install -r requirements.txt

# 3. place startup_founder_burnout_2026.csv in the same folder as the notebook

# 4a. run the notebook
jupyter notebook startup_founder_burnout_analysis.ipynb   # then Run All

# 4b. or run the script
python startup_founder_burnout_analysis.py
```

Outputs (final CSV and SQLite database) are saved in an `outputs/` folder. To use the **risk calculator**, double-click `startup_failure_risk_calculator.html` to open it in a browser (an internet connection is needed to load Tailwind CSS and Chart.js).

## Key findings

- **23.7%** of startups are flagged as likely failures.
- Failure rate rises sharply with burnout: **7.9%** (low), **35.6%** (moderate), **69.0%** (severe).
- Economic climate matters: **45.7%** failure in a Recession and **35.8%** in a Funding Winter, against about **14%** in a Stable Economy or Bull Market.
- Strongest drivers of shutdown probability: burnout, employee turnover, co-founder conflict and long working hours increase it; work-life balance, runway and product-market fit reduce it.
- In the calculator model, investor pressure has almost no independent effect once the other variables are included.

## Notes and limitations

- The associations are correlational, not causal. For example, founders who seek mental-health support show a higher failure rate (30.6% vs 21.2%), which most likely reflects that struggling founders seek help, not that support causes failure.
- `Shutdown_Risk` and `Startup_Failure_Flag` are derived directly from `Shutdown_Probability`, so they must never be used as predictors of it.
- The calculator is an educational simulator, not financial advice.

## Author

`<Makarand A Bhambure>`
