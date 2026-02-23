# Copilot Instructions for FY2026_Feb

## Project Overview

This is a **data analytics and machine learning learning repository** containing Jupyter notebooks focused on practical data science techniques and analysis workflows. The project covers core ML preprocessing, feature engineering, statistical testing, and time series forecasting.

## Key Patterns & Conventions

### Data Science Workflow Structure

Each notebook follows a consistent pattern:
1. **Imports** - Standard stack: `pandas`, `numpy`, `matplotlib`, `seaborn`, `sklearn`
2. **Data Loading** - CSV files loaded via `pd.read_csv()` into DataFrames
3. **EDA** - Exploratory Data Analysis with `df.shape`, `df.info()`, `df.describe()`
4. **Data Cleaning** - Handle nulls (`fillna`), remove duplicates, type conversion
5. **Feature Engineering** - Apply transformations, encoding, scaling
6. **Analysis/Visualization** - Create plots with `matplotlib`/`seaborn`

### Core Technical Areas

#### 1. **Data Encoding** (`Encoding.ipynb`)
- **One-Hot Encoding**: Use `sklearn.preprocessing.OneHotEncoder` or `pd.get_dummies()` for nominal (unordered) categorical data
- **Label/Ordinal Encoding**: Use `LabelEncoder` for ordered categories or `OrdinalEncoder` with explicit category ordering
- **Target Encoding**: Map categorical values to target variable means via `groupby().mean().to_dict()` and `map()`
- Pattern: Always specify category order explicitly for ordinal encoding to avoid surprises

#### 2. **Feature Scaling** (`Scaling.ipynb`)
- **Standardization**: Z-score normalization using `StandardScaler` (mean=0, std=1)
  - Manual formula: `(x - mean) / std`
- **Normalization**: Min-Max scaling to [0,1] range
- **Unit Vector Scaling**: L2 normalization
- Convention: Scaling does NOT change data distribution—verify with plots before/after
- Always suppress warnings: `warnings.filterwarnings("ignore")`

#### 3. **Data Quality** (`HR_Analytics.ipynb`, `Kidney_Disease.ipynb`)
- Handle null values: `fillna()` with reasonable defaults (not always "0")
- Remove duplicates: `drop_duplicates(inplace=True)`
- Type conversion for mixed columns: `pd.to_numeric(col, errors='coerce')` for columns with non-numeric values
- Document quality issues with comments inline

#### 4. **Time Series Analysis** (`Weather_Forecasting_project.ipynb`)
- **Data Preparation**: Set date column as index `df.set_index("date")`
- **Stationarity Testing**: Use ADF test from `statsmodels.tsa.stattools.adfuller()`
- **Decomposition**: `seasonal_decompose()` for trend/seasonality extraction
- **Forecasting Models**: ARIMA and SARIMAX from `statsmodels.tsa`
- Pattern: Always check stationarity before ARIMA (p-value ≤ 0.05 = stationary)

### File Organization

```
FY2026_Feb/
├── Notebook files (tutorials)
│   ├── Encoding.ipynb (3 techniques: one-hot, ordinal, target)
│   ├── Scaling.ipynb (feature scaling methods)
│   ├── HR_Analytics.ipynb (complete EDA pipeline)
│   ├── Kidney_Disease.ipynb (data quality + classification)
│   ├── Weather_Forecasting_project.ipynb (time series ARIMA)
│   ├── files.ipynb, final_quiz.ipynb, google_play.ipynb
│   └── CSGO_by_Ujjwal_2.ipynb, online_retail.ipynb
├── Data files (CSVs)
│   ├── HRDataset_v14.csv
│   ├── kidney_disease.csv
│   ├── OnlineRetail.csv
│   └── googleplaystore.csv
├── Documentation
│   └── 📘 A_B Testing_A Complete Guide for Data Analysts.md
└── .github/copilot-instructions.md (this file)
```

### Common Imports Pattern

Notebooks typically start with:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')

# Domain-specific imports added as needed
from sklearn.preprocessing import OneHotEncoder, LabelEncoder, StandardScaler
from statsmodels.tsa.arima.model import ARIMA
```

### Notebook Cell Patterns

- **Single-responsibility cells**: Each cell should demonstrate ONE concept
- **Data inspection cells**: Frequent use of `df.head()`, `df.shape`, `df.info()` to verify state
- **Visualization cells**: Many cells just display outputs (e.g., `df`, plots) for interactive verification
- **Comments with examples**: Cells often include comments showing input/output examples
- **No assertion testing**: Learning notebooks skip formal testing in favor of visual inspection

## Development Guidelines for AI Agents

### When Adding Analysis Code

1. **Maintain the EDA-first pattern**: Always start with data exploration before transformation
2. **Add intermediate verification cells**: Insert DataFrame displays after major transformations
3. **Document transformations inline**: Add comments explaining WHY, not just WHAT
4. **Use built-in pandas/sklearn methods**: Avoid custom implementations of standard techniques
5. **Handle data quality explicitly**: Never silently drop missing values—show the counts first

### When Modifying Encoding/Scaling

- Preserve the dual approach pattern (e.g., both `OneHotEncoder` and `pd.get_dummies()` shown)
- Add example data frames showing before/after transformations
- Include the underlying formula/theory as comments
- Test with both fit/transform and transform workflows

### When Working with Datasets

- CSV files should be in the root directory (`/Users/sangameshwaruppe/FY2026_Feb/FY2026_Feb/`)
- Always verify file paths are relative for notebook reproducibility
- Check for encoding issues with `pd.to_numeric(errors='coerce')` for numeric columns
- Document dataset shape and unique value counts early

## Known Dependencies

**Core Data Science Stack:**
- `pandas` - DataFrames and data manipulation
- `numpy` - Numerical operations
- `sklearn` - Preprocessing, encoding, scaling
- `matplotlib`, `seaborn` - Visualization
- `statsmodels` - Time series and statistical tests

**Note:** No external requirements.txt exists; packages are imported inline

## No Formal Testing Approach

This is an educational repository focused on interactive notebooks. There are no unit tests or CI/CD pipelines—evaluation is manual through notebook output inspection and visualizations.
