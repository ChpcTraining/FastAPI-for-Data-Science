# Lesson 8 — Generating Statistics

## Goal

Generate descriptive statistics using Pandas.

```python
summary = df.describe()
print(summary)
```

Convert the summary to HTML:

```python
summary_table = df.describe().to_html()
```

Pass it to the template:

```python
context={
    "table": table,
    "summary": summary_table
}
```

HTML:

```html
<h2>Statistical Summary</h2>
{{ summary | safe }}
```

## Explore

Try:

```python
df.mean(numeric_only=True)
df.min(numeric_only=True)
df.max(numeric_only=True)
df.isnull().sum()
```

## Exercise

Display the number of missing values for each column.
