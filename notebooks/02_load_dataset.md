
# 02 Load Dataset with Python

## Purpose

The purpose of this step is to load the Eskom historical hourly demand dataset using Python and pandas.

The dataset used in this project is:

- File name: ESK19242.csv
- Source: Eskom Data Portal
- Rows: 37,560
- Columns: 5

## What is pandas?

pandas is a Python library used to work with table data, similar to Excel spreadsheets.

In this project, pandas will help us:

- read the CSV file
- inspect rows and columns
- clean column names
- convert date values
- handle missing values
- prepare the dataset for analysis and modelling

## Step 1: Import pandas

```python
import pandas as pd
```

This line loads the pandas library and gives it the shorter name `pd`.

## Step 2: Load the CSV file

```python
df = pd.read_csv("ESK19242.csv")
```

This line reads the CSV file and stores it in a variable called `df`.

The name `df` means DataFrame. A DataFrame is a table of data in pandas.

## Step 3: View the first rows

```python
df.head()
```

This displays the first five rows of the dataset.

## Step 4: Check the size of the dataset

```python
df.shape
```

Expected output:

```text
(37560, 5)
```

This means the dataset has:

- 37,560 rows
- 5 columns

## Step 5: Check column names

```python
df.columns
```

Expected columns:

```text
Date Time Hour Beginning
Residual Forecast
RSA Contracted Forecast
Residual Demand
RSA Contracted Demand
```

## Step 6: Check data types

```python
df.dtypes
```

Expected result:

```text
Date Time Hour Beginning     object
Residual Forecast           float64
RSA Contracted Forecast     float64
Residual Demand             float64
RSA Contracted Demand       float64
```

Important observation:

The date column is currently stored as `object`, which means Python is treating it as text. Later, we need to convert it into a proper date-time format.

## Step 7: Check missing values

```python
df.isna().sum()
```

Expected result:

```text
Date Time Hour Beginning     0
Residual Forecast            0
RSA Contracted Forecast      0
Residual Demand             48
RSA Contracted Demand       48
```

This tells us that the actual demand columns have 48 missing values.

## What we learned

The dataset loaded successfully.

Initial inspection shows that:

- the dataset has 37,560 hourly records;
- the date column needs conversion;
- the demand and forecast columns are numeric;
- the actual demand columns contain 48 missing values;
- the dataset is suitable for time-series analysis and forecasting.
