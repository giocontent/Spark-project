# Gas Prices Analysis in France (2022-2024)

Analysis of gas station prices across France using PySpark for distributed data processing, visualization, and machine learning.

## Authors 
- Giovanni Contento
- Egle Caudullo

## Project Overview

This project analyzes three years of daily gas price data from French stations to understand pricing patterns and build forecasting models. The analysis includes data processing with Spark, temporal visualizations, and ML-based price predictions.


## Data Source

Data from [rvm-courses/GasPrices](https://github.com/rvm-courses/GasPrices):
- Daily price updates (2022-2024)
- Station locations and metadata
- Service information

The 2022 dataset is split into two files due to size.

## Analysis Pipeline

### 1. Data Collection & Preparation
- Load and merge gas price files from multiple years
- Parse dates into year, month, week components
- Fix coordinate formats for geographic visualization
- Create Spark SQL views for analysis

### 2. Feature Engineering
- **Price Index**: Normalized prices relative to national average
  ```
  Price_Index = 100 × (Station_Price - National_Avg) / (National_Avg + 1)
  ```
- **Week Index**: Sequential week numbering from start of dataset
- Filter out fuel types with insufficient data

### 3. Visualization
- Weekly price evolution by fuel type
- Time series showing national trends
- Optional: Geographic heat maps at department level (Folium)

### 4. Predictive Modeling
- Build ML pipeline with Spark MLlib
- Use lag features (previous day prices) for forecasting
- Models: LinearRegression, RandomForestRegressor
- Evaluation with RMSE and actual vs predicted plots

The focus is on a working pipeline rather than optimal accuracy.

## Key Features

**Technologies:**
- PySpark (data processing)
- Spark SQL (queries)
- Spark MLlib (machine learning)
- Matplotlib/Seaborn (visualization)

**Approach:**
- Distributed computing for large datasets
- Lag-based features instead of traditional time series models
- Modular notebook structure with markdown documentation

## Requirements

```
pyspark>=3.3.0
pandas
numpy
matplotlib
seaborn
```

Optional for mapping:
```
folium
geopandas
```

## Running the Notebook

Launch Spark locally:
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("GasPriceAnalysis") \
    .getOrCreate()
```

Then run cells sequentially. Data files should be in `data/` directory.

## Results

The analysis reveals:
- Temporal patterns in fuel pricing across France
- Regional price variations through geographic analysis
- Reasonable next-day price predictions using lag features
- Impact of fuel type on price volatility

## Notes

This was a mini-project for a distributed computing course. The emphasis is on Spark workflows and scalable data processing rather than achieving production-level prediction accuracy.

