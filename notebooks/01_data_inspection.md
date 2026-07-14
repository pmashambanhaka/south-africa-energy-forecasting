# 01 Data Inspection

## Dataset Used

Dataset name: Eskom historical hourly demand data  
Source: Eskom Data Portal  
File received: ESK19242.csv

## Purpose of the Dataset

This dataset will be used to analyse and forecast South African electricity demand using historical hourly demand and forecast values.

## Initial Dataset Structure

The dataset contains hourly electricity demand and forecast values for South Africa.

Columns identified:

- Date Time Hour Beginning
- Residual Forecast
- RSA Contracted Forecast
- Residual Demand
- RSA Contracted Demand

## Dataset Size

The dataset contains:

- 37,560 rows
- 5 columns

## Date Range

The dataset covers the period:

- Start: 1 April 2022 00:00
- End: 13 July 2026 23:00

The data is recorded hourly.

## Missing Values

Initial inspection shows that the actual demand columns contain some missing values:

- Residual Demand: 48 missing values
- RSA Contracted Demand: 48 missing values

The forecast columns do not contain missing values.

This suggests that the final part of the dataset may contain forecast records where actual demand values were not yet available.

## Main Target Variable

For the first version of this project, the main target variable will be:

- RSA Contracted Demand

This column represents the actual contracted demand and will be used for exploratory analysis and forecasting.

## Initial Observations

The dataset is suitable for a portfolio-level time-series forecasting project because it contains more than four years of hourly electricity demand data.

The data can support analysis of:

- Hourly demand patterns
- Daily demand cycles
- Weekly trends
- Seasonal patterns
- Forecast versus actual demand comparison
- Baseline forecasting model development

## Next Steps

- Load the dataset using Python and pandas
- Convert the date column into datetime format
- Rename columns into cleaner Python-friendly names
- Separate rows with actual demand from rows with forecast-only values
- Plot demand over time
- Analyse hourly, daily, weekly, and monthly demand patterns
