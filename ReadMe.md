# Learning Data Manipulation with Pandas

This repository tracks my journey learning data manipulation using the **pandas** library in Python. I’m using Jupyter Notebook to experiment with code and GitHub to store my progress. Below is what I’ve learned so far about pandas and how I’m applying it.
## What I Understand About Pandas
- **Pandas Basics**: Pandas is a Python library for working with data in tables (called DataFrames). I can load data, explore it, and manipulate it.
- **Exploring Data**:
  - `df.head()`: Shows the first 5 rows (or `df.tail()` for the last 5) to preview my data.
  - `df.sample(n)`: Picks random rows—good for a quick look at big datasets.
  - `df.info()`: Tells me about columns, data types, and missing values.
  - `df.dtypes`: Lists data types of each column.
  - `df.shape`: Shows how many rows and columns I have (e.g., `(rows, columns)`).
  - `df.describe()`: Gives stats (mean, min, max) for numeric columns.
  - `df.columns`: Lists all column names.
- **Common Operations**:
  - **Counting Values**: `df["column_name"].value_counts()` counts unique values in a column.
  - **Correlation**: `df.corr()` finds correlations, but only for numeric columns—I filter with `select_dtypes()`.
- **Fixing Errors**: [Keep your existing error notes here]
- **Fixing Errors**:
  - If I get a `ValueError: could not convert string to float`, it means I tried `corr()` on a column with strings (like dates). I can fix it by excluding those columns.
  - If I see `AttributeError: 'Series' object has no attribute 'sales_counts'`, it’s because I typed the wrong method name. I meant `value_counts()`, not `sales_counts()`.

## Tools I’m Using
- **Jupyter Notebook**: Where I write and test my pandas code. I save my work as `.ipynb` files.
- **GitHub**: I’m learning to push my notebooks here to share and back up my work. Steps I’ve learned:
  1. Save my notebook.
  2. Use `git add`, `git commit`, and `git push` in the terminal to upload it.
  3. Connect my local folder to a GitHub repo with `git remote add origin <url>`.

## My Next Steps
- Learn how to clean messy data (e.g., missing values or wrong formats).
- Figure out how to join or merge multiple DataFrames.
- Practice making plots with pandas and other libraries like Matplotlib.

## Example Code
Here’s a snippet of what I’ve tried:
```python
import pandas as pd

# Sample DataFrame
df = pd.DataFrame({
    "DocumentDate": ["2014-09-16", "2014-09-17", "2014-09-16"],
    "sales": [100, 150, 200]
})

# Count unique dates
print(df["DocumentDate"].value_counts())

# Correlation (only numeric columns)
numeric_df = df.select_dtypes(include=['int64', 'float64'])
print(numeric_df.corr())