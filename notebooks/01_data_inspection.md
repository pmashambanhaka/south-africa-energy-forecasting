# 01 Data Inspection

## Dataset Used

Dataset name: System hourly actual and forecasted demand  
Source: Eskom Data Portal  
File: System_hourly_actual_and_forecasted_demand.csv

## Initial Dataset Structure

The dataset contains hourly electricity demand and forecast values for South Africa.

Columns identified:

- DateTimeKey
- Residual Forecast
- RSA Contracted Forecast
- Residual Demand
- RSA Contracted Demand

## Initial Observations

The dataset contains both actual demand values and forecast demand values.

Actual demand values are available for the period:

- 2 July 2026 to 7 July 2026

Forecast values are available for the period:

- 8 July 2026 to 15 July 2026

This means the dataset is useful for understanding the structure of electricity demand data, but a longer historical dataset will be needed for a stronger machine learning forecasting model.

## Next Steps

- Load the dataset using Python and pandas
- Convert DateTimeKey into a datetime format
- Clean column names
- Separate actual demand data from forecast data
- Plot hourly demand patterns
- Identify whether a larger historical dataset is available
