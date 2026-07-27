# Electricity Weather Forecasting

Prediction of daily electricity consumption from weather and calendar data.

## Overview

This project explores how weather conditions can be used to estimate daily electricity consumption. The workflow covers data exploration, cleaning, feature engineering, baseline modeling, and model comparison.

The final models use weather variables such as temperature, wind speed, precipitation, and derived seasonal indicators to predict total daily electricity consumption.

## Dataset

The dataset comes from Kaggle:

[Electricity consumption based on weather data](https://www.kaggle.com/datasets/sudhirsingh27/electricity-consumption-based-on-weather-data)

Each row represents one day. The dataset covers approximately four years, from December 2006 to November 2010.

Main columns:

- `date`: observation date
- `AWND`: average daily wind speed
- `PRCP`: daily precipitation
- `TMAX`: daily maximum temperature
- `TMIN`: daily minimum temperature
- `daily_consumption`: total daily electricity consumption

## Project Structure

```text
.
├── data/
│   ├── electricity_consumption_based_weather_dataset.csv
│   └── processed/
│       ├── electricity_weather_cleaned.csv
│       └── electricity_weather_features.csv
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_baseline_model.ipynb
│   └── 05_model_comparison.ipynb
├── reports/
├── src/
├── requirements.txt
└── README.md
```

## Methodology

### Data Exploration

The exploratory analysis focuses on:

- dataset structure and column types;
- missing values;
- descriptive statistics;
- daily consumption trends over time;
- seasonal and weekday patterns;
- relationships between weather variables and electricity consumption;
- correlations between numerical variables.

The initial analysis shows a clear seasonal pattern, with higher electricity consumption during colder periods. Weekend consumption is also higher on average.

### Data Cleaning

The cleaning step includes:

- converting the `date` column to datetime format;
- inspecting missing values;
- filling missing `AWND` values using linear interpolation;
- detecting consumption outliers with the IQR method;
- flagging unusually low consumption values;
- exporting a cleaned dataset.

The raw dataset is kept unchanged.

### Feature Engineering

Additional features are created to capture calendar and weather effects:

- `year`
- `month`
- `day_of_week`
- `day_of_year`
- `is_weekend`
- `temperature_range`
- `temperature_mean`
- `heating_degree_days`
- `cooling_degree_days`

These features are saved in:

```text
data/processed/electricity_weather_features.csv
```

### Modeling

A time-based train/test split is used:

- training set: observations before 2010;
- test set: observations from 2010 onward.

The baseline model is a linear regression. It is then compared with two tree-based models:

- Random Forest
- Gradient Boosting

The models are evaluated using:

- MAE
- RMSE
- R² score

## Results

The linear regression baseline captures part of the seasonal trend but struggles with abrupt daily changes and extreme values.

Gradient Boosting performs best among the tested models, with the lowest RMSE and the highest R² score. The improvement over the baseline is present but limited, suggesting that weather and calendar features explain only part of the variation in daily electricity consumption.

Future improvements could include additional predictors such as:

- lagged electricity consumption;
- holidays;
- occupancy or activity indicators;
- electricity prices;
- more detailed weather variables.

## How to Run

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Then open and run the notebooks in order from the `notebooks/` folder.

## Tools

- Python
- pandas
- NumPy
- matplotlib
- seaborn
- scikit-learn
- Git
- GitHub
