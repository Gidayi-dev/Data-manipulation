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

Here’s an explanation of different join concepts in pandas with code examples:

### 1. **Inner Join**  
An inner join returns only the rows where there is a match in both DataFrames.

```python
import pandas as pd

df1 = pd.DataFrame({'id': [1, 2, 3], 'name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'id': [2, 3, 4], 'age': [25, 30, 22]})

merged_inner = pd.merge(df1, df2, on='id', how='inner')
print(merged_inner)
```

**Output:**
```
   id   name  age
0   2    Bob   25
1   3  Charlie   30
```

---

### 2. **Left Join**  
A left join keeps all rows from the left DataFrame and fills missing values with `NaN` from the right DataFrame.

```python
merged_left = pd.merge(df1, df2, on='id', how='left')
print(merged_left)
```

**Output:**
```
   id   name   age
0   1  Alice   NaN
1   2    Bob  25.0
2   3  Charlie 30.0
```

---

### 3. **Right Join**  
A right join keeps all rows from the right DataFrame and fills missing values from the left DataFrame.

```python
merged_right = pd.merge(df1, df2, on='id', how='right')
print(merged_right)
```

**Output:**
```
   id   name  age
0   2    Bob   25
1   3  Charlie   30
2   4     NaN   22
```

---

### 4. **Outer Join**  
An outer join keeps all rows from both DataFrames and fills missing values with `NaN`.

```python
merged_outer = pd.merge(df1, df2, on='id', how='outer')
print(merged_outer)
```

**Output:**
```
   id   name   age
0   1  Alice   NaN
1   2    Bob  25.0
2   3  Charlie 30.0
3   4     NaN  22.0
```

---

### 5. **Merging on Index**  
Instead of merging on a specific column, you can merge on the index.

```python
df1.set_index('id', inplace=True)
df2.set_index('id', inplace=True)

merged_index = df1.join(df2, how='inner')
print(merged_index)
```

---

