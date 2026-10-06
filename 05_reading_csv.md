# Lesson 5 — Reading CSV Data

## Goal

Read and inspect a CSV using Pandas.

```python
import pandas as pd

df = pd.read_csv("data/students.csv")

print(df)
```

Useful operations:

```python
df.head()
df.columns
df.shape
df.describe()
```

`df.shape` returns `(rows, columns)`.

For example:

```python
print(df.shape)
```

could return:

```text
(5, 3)
```

## Exercise

Print:

- The first three rows
- All column names
- Number of rows
- Number of columns
