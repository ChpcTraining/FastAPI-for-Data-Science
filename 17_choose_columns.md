# Lesson 17 — Letting the User Choose Columns

## Goal

Build HTML controls from DataFrame column names.

Get the columns:

```python
columns = df.columns.tolist()
```

Pass them to Jinja:

```python
context={
    "columns": columns
}
```

Create a dropdown:

```html
<label>X Column</label>

<select name="x_column">
    {% for column in columns %}
        <option value="{{ column }}">
            {{ column }}
        </option>
    {% endfor %}
</select>
```

Create another dropdown for the Y column:

```html
<label>Y Column</label>

<select name="y_column">
    {% for column in columns %}
        <option value="{{ column }}">
            {{ column }}
        </option>
    {% endfor %}
</select>
```

You can also create a plot-type selector:

```html
<select name="plot_type">
    <option value="scatter">Scatter</option>
    <option value="line">Line</option>
    <option value="bar">Bar</option>
</select>
```

## Key concept

```text
DataFrame columns → Python list → Jinja loop → HTML dropdown
```
