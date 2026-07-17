# 03 Clean Dataset

## Purpose

The purpose of this step is to clean the Eskom historical hourly demand dataset so it can be used for analysis and forecasting.

The raw dataset contains long column names and a date column that must be converted into a proper datetime format.

## Step 1: Import pandas

```python
import pandas as pd
```

pandas is used to read, clean, and prepare the dataset.

## Step 2: Load the Dataset

```python
df = pd.read_csv("ESK19242.csv")
```

This loads the raw Eskom CSV file into a pandas DataFrame called `df`.

## Step 3: Rename Columns

```python
df = df.rename(columns={
    "Date Time Hour Beginning": "datetime",
    "Residual Forecast": "residual_forecast",
    "RSA Contracted Forecast": "rsa_contracted_forecast",
    "Residual Demand": "residual_demand",
    "RSA Contracted Demand": "rsa_contracted_demand"
})
```

The original column names are long and contain spaces.

Renaming them makes the dataset easier to work with in Python.

For example:

- `Date Time Hour Beginning` becomes `datetime`
- `RSA Contracted Demand` becomes `rsa_contracted_demand`

## Step 4: Convert Date Column

```python
df["datetime"] = pd.to_datetime(df["datetime"])
```

This converts the `datetime` column from text into a proper date-time format.

This is important because time-series analysis requires Python to understand dates and hours correctly.

## Step 5: Sort the Data by Date

```python
df = df.sort_values("datetime")
```

This ensures that the dataset is arranged in chronological order from the earliest date to the latest date.

## Step 6: Remove Rows with Missing Actual Demand

```python
df_actual = df.dropna(subset=["rsa_contracted_demand"]).copy()
```

The final part of the dataset contains some missing actual demand values.

For the first analysis, we only use rows where actual demand is available.

The cleaned dataset is stored in a new DataFrame called `df_actual`.

## Step 7: Create Time-Based Features

```python
df_actual["hour"] = df_actual["datetime"].dt.hour
df_actual["day"] = df_actual["datetime"].dt.day
df_actual["day_of_week"] = df_actual["datetime"].dt.dayofweek
df_actual["month"] = df_actual["datetime"].dt.month
df_actual["year"] = df_actual["datetime"].dt.year
df_actual["date"] = df_actual["datetime"].dt.date
```

These new columns help us analyse electricity demand patterns.

They allow us to answer questions such as:

- Does demand change by hour of the day?
- Is demand different during weekdays and weekends?
- Are there seasonal patterns across months?
- How has demand changed across years?

## Step 8: Check the Cleaned Dataset

```python
df_actual.head()
```

This shows the first five rows of the cleaned dataset.

```python
df_actual.shape
```

This shows the number of rows and columns after removing missing actual demand values.

```python
df_actual.isna().sum()
```

This checks whether any missing values remain in the cleaned dataset.

## Step 9: Optional Save Processed Dataset

```python
df_actual.to_csv("eskom_hourly_demand_cleaned.csv", index=False)
```

This saves the cleaned dataset as a new CSV file.

For this project, the cleaned CSV file should be kept locally and not uploaded to GitHub.

## What We Learned

In this step, we cleaned the raw Eskom dataset by:

- renaming columns;
- converting the date column;
- sorting the data by time;
- removing rows with missing actual demand values;
- creating time-based features for analysis.

The dataset is now ready for exploratory data analysis.
