# Lesson 7 — Displaying a Data Table

## Goal

Convert a Pandas DataFrame into an HTML table.

```python
table = df.to_html(index=False)
```

Pass it to the template:

```python
context={
    "table": table
}
```

HTML:

```html
<h2>Dataset</h2>
{{ table | safe }}
```

`safe` tells Jinja to render the generated table as HTML rather than plain text.

For large datasets, preview only a small number of rows:

```python
table = df.head(20).to_html(index=False)
```

## Exercise

Change the preview to show only the first 10 rows.
