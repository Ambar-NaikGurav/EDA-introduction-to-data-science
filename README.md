# Cafe Sales: Exploratory Data Analysis (EDA)

This project contains a comprehensive Exploratory Data Analysis (EDA) performed on a messy, real-world transactional dataset from a cafe (`cafe_sales_dirty.csv`). 

The primary goal of this project is to demonstrate foundational data science techniques, including robust data cleaning, statistical imputation, and generating insightful visualizations to drive business decisions.

## 📂 Project Structure

- `cafe_sales_dirty.csv`: The raw, unprocessed transactional dataset containing missing values and string errors.
- `cafe_sales_cleaned.csv`: The finalized dataset after applying advanced data cleaning and imputation pipelines.
- `pdf_exact_eda.py`: The core Python script that performs the data cleaning and generates the visualizations.
- `cafe_analysis.ipynb`: A Jupyter Notebook containing the same analytical steps for interactive exploration.

## 🧹 Data Cleaning & Preprocessing

The raw dataset contained multiple anomalies (e.g., text like `"ERROR"` or `"UNKNOWN"` in numerical columns) and significant missing data. Our cleaning pipeline handles this by:
1. **String Standardization**: Replacing all anomalous string entries with `NaN`.
2. **Chronological Sorting**: Converting string dates to datetime objects and sorting the transactions temporally.
3. **Advanced Imputation**:
   - *Prices*: Grouping by specific items and applying forward/backward filling (`ffill`, `bfill`) to accurately reconstruct historical menu prices.
   - *Quantities*: Filling missing quantities with the median quantity of that specific item, rather than a flawed global median.
   - *Derived Metrics*: Recalculating missing `Total Spent` deterministically (`Quantity * Price Per Unit`).
   - *Categoricals*: Filling independent missing categorical values (like Payment Method or Location) with the mode.
4. **Type Optimization**: Converting columns into memory-efficient pandas types (`category`, `int32`, `float32`).

By using robust statistical imputation instead of naively dropping rows, we successfully retained **100% of the original 10,000 transactions**.

## 📊 Exploratory Data Analysis

The EDA pipeline generates a suite of Seaborn and Matplotlib visualizations designed to extract actionable business insights:
- **Univariate Analysis**: Bar charts identifying the most popular and frequently sold items.
- **Bivariate Distributions**: Segmented boxplots uncovering the statistical spread (medians, quartiles, outliers) of quantities and pricing across different items.
- **Correlation Matrices**: Heatmaps verifying the mathematical relationships between transactional metrics.
- **Time-Series Revenue Analysis**: Line plots tracking monthly revenue trends across the entire year of 2023.
- **Business Insights**: Extra visualizations breaking down revenue by `Location` (In-store vs Takeaway), preferred `Payment Methods`, and `Day of the Week` sales patterns.

## 🚀 Getting Started

### Prerequisites
- Python 3.x
- Pandas
- Matplotlib
- Seaborn

### Running the Analysis
You can execute the entire analysis pipeline by running the provided Python script:
```bash
python pdf_exact_eda.py
```
This will automatically load the cleaned data, compute the statistical aggregations, print out the top-performing categories, and display the visualization plots one by one.
