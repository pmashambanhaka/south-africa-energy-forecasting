# 04 Exploratory Data Analysis

## Purpose

The purpose of this step is to explore the cleaned Eskom hourly demand dataset.

Exploratory Data Analysis helps us understand patterns in the data before building a forecasting model.

In this project, we want to analyse electricity demand by time, hour, day, month, and year.

## Step 1: Import Required Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
```

pandas is used for data analysis.

matplotlib is used to create charts.

## Step 2: Load the Dataset

```python
df = pd.read_csv("ESK19242.csv")
```

This loads the Eskom demand dataset.

## Step 3: Clean the Dataset

```python
df = df.rename(columns={
    "Date Time Hour Beginning": "datetime",
    "Residual Forecast": "residual_forecast",
    "RSA Contracted Forecast": "rsa_contracted_forecast",
    "Residual Demand": "residual_demand",
    "RSA Contracted Demand": "rsa_contracted_demand"
})

df["datetime"] = pd.to_datetime(df["datetime"])

df = df.sort_values("datetime")

df_actual = df.dropna(subset=["rsa_contracted_demand"]).copy()
```

This prepares the dataset for analysis.

It renames columns, converts the date column, sorts the data, and removes rows where actual demand is missing.

## Step 4: Create Time Features

```python
df_actual["hour"] = df_actual["datetime"].dt.hour
df_actual["day"] = df_actual["datetime"].dt.day
df_actual["day_of_week"] = df_actual["datetime"].dt.dayofweek
df_actual["month"] = df_actual["datetime"].dt.month
df_actual["year"] = df_actual["datetime"].dt.year
df_actual["date"] = df_actual["datetime"].dt.date
```

These columns allow us to analyse demand patterns across time.

## Step 5: Summary Statistics

```python
df_actual["rsa_contracted_demand"].describe()
```

This shows basic statistics for electricity demand.

It includes:

- count
- average demand
- minimum demand
- maximum demand
- standard deviation

## Step 6: Plot Demand Over Time

```python
plt.figure(figsize=(12, 5))
plt.plot(df_actual["datetime"], df_actual["rsa_contracted_demand"])
plt.title("RSA Contracted Demand Over Time")
plt.xlabel("Date")
plt.ylabel("Demand")
plt.show()
```

This chart shows how electricity demand changes over time.

It helps us see long-term patterns, spikes, and dips.

## Step 7: Average Demand by Hour

```python
hourly_demand = df_actual.groupby("hour")["rsa_contracted_demand"].mean()

plt.figure(figsize=(10, 5))
hourly_demand.plot(kind="line")
plt.title("Average Demand by Hour of Day")
plt.xlabel("Hour of Day")
plt.ylabel("Average Demand")
plt.show()
```

This chart shows the average electricity demand for each hour of the day.

It helps identify peak demand hours.

## Step 8: Average Demand by Day of Week

```python
weekday_demand = df_actual.groupby("day_of_week")["rsa_contracted_demand"].mean()

plt.figure(figsize=(10, 5))
weekday_demand.plot(kind="bar")
plt.title("Average Demand by Day of Week")
plt.xlabel("Day of Week")
plt.ylabel("Average Demand")
plt.show()
```

This chart compares demand across different days of the week.

In Python:

```text
0 = Monday
1 = Tuesday
2 = Wednesday
3 = Thursday
4 = Friday
5 = Saturday
6 = Sunday
```

## Step 9: Average Demand by Month

```python
monthly_demand = df_actual.groupby("month")["rsa_contracted_demand"].mean()

plt.figure(figsize=(10, 5))
monthly_demand.plot(kind="bar")
plt.title("Average Demand by Month")
plt.xlabel("Month")
plt.ylabel("Average Demand")
plt.show()
```

This chart helps us understand seasonal demand patterns.

## Step 10: Average Demand by Year

```python
yearly_demand = df_actual.groupby("year")["rsa_contracted_demand"].mean()

plt.figure(figsize=(10, 5))
yearly_demand.plot(kind="bar")
plt.title("Average Demand by Year")
plt.xlabel("Year")
plt.ylabel("Average Demand")
plt.show()
```

This chart helps compare demand across different years.

## What We Are Looking For

During exploratory analysis, we look for:

- daily demand patterns;
- hourly peak demand periods;
- weekday and weekend differences;
- seasonal demand patterns;
- unusual spikes or drops;
- long-term changes in demand.

## What We Learned

Exploratory Data Analysis helps us understand the behaviour of electricity demand before building a forecasting model.

The findings from this step will guide the forecasting approach.
