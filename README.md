# Mexico Real Estate Analysis

This repository demonstrates a complete workflow for preparing, exploring, visualizing and modeling a real-estate dataset from Mexico. The work is organized into four Jupyter notebooks: **cleaning**, **analysis**, **plot**, and **machine-learning**.

## Dataset

The raw data was originally split across three CSV files with slightly different formats:

- `mexico-real-estate-1.csv` – price strings with `$` and commas
- `mexico-real-estate-2.csv` – prices in MXN requiring conversion
- `mexico-real-estate-3.csv` – location data embedded in a single field

A combined file, `mexico-real-estate-combined.csv`, is produced by the cleaning notebook and used by the subsequent analysis notebooks.

Key columns appearing across the dataset:

- `state` – Mexican state of the listing
- `property_type` – e.g. house, apartment, lot
- `price_usd` – price converted to US dollars
- `area_m2` – area of property in square meters
- `lat` / `lon` – geographic coordinates (when available)

## Notebook Details

### 1. `cleaning.ipynb`

This notebook standardizes and merges the three source files:

- Load each CSV with `pandas`.
- Drop rows with missing values.
- Normalize `price_usd`: strip currency symbols, convert MXN to USD, and cast to float.
- Extract `state` and split latitude/longitude when needed.
- Concatenate the cleaned DataFrames and save the result as `mexico-real-estate-combined.csv`.

This step ensures all later notebooks work with a consistent schema.

### 2. `analysis.ipynb`

Exploratory data analysis using the combined dataset:

1. Load the cleaned CSV and display the full DataFrame.
2. Compute frequency counts of listings by state (top 10).
3. Aggregate total price by state and by property type.
4. Build pivot tables to examine price distributions across states and property types.
5. Generate descriptive statistics (`count`, `mean`, `std`, etc.) overall, by state, and by property type.

Output is printed to the notebook for inspection.

### 3. `plot.ipynb`

Visualizations for insights and distribution patterns:

- Pie chart showing proportion of total price by property type.
- Histograms and box plots for `area_m2` and `price_usd` distributions.
- Interactive scatter map (Plotly) with properties colored and sized by price.
- Compute `price_per_m2` and bar-plot average values by state.
- Conduct linear regression and plot price vs. area correlation.
- Isolate Mexico City (`Distrito Federal`) properties to examine local correlation.

These visualizations aid in understanding price/area relationships and geographic patterns.

### 4. `machine-learning.ipynb`

A simple regression model predicting price from area:

- Use `scipy.stats.linregress` to print slope, intercept, and R².
- Split data into training/test sets with `sklearn.model_selection.train_test_split`.
- Fit a `LinearRegression` model and evaluate its score.
- Plot the regression line against the test points.

This notebook demonstrates a basic predictive modeling workflow.

## Reproducing the Workflow

1. Clone or download the repository.
2. Create/activate a Python virtual environment and install dependencies:
   ```bash
   pip install pandas matplotlib plotly scikit-learn scipy
   ```
3. Run `cleaning.ipynb` first to generate `mexico-real-estate-combined.csv`.
4. Execute the other notebooks in order: `analysis.ipynb`, `plot.ipynb`, `machine-learning.ipynb`.
5. You can modify or extend the analysis as desired (e.g. add more plots, try different models).

---

This README documents the full processing pipeline. Feel free to expand it with additional sections (e.g. data sources, future work, license) as the project evolves.