# Lesson 6 — Displaying Dataset Information

## Goal

Use Pandas in a FastAPI route and display dataset information.

```python
@app.get("/")
def home(request: Request):
    df = pd.read_csv("data/students.csv")

    rows = df.shape[0]
    columns = df.shape[1]

    return templates.TemplateResponse(
        request=request,
        name="index.html",
        context={
            "rows": rows,
            "columns": columns
        }
    )
```

HTML:

```html
<h2>Dataset Information</h2>
<p>Rows: {{ rows }}</p>
<p>Columns: {{ columns }}</p>
```

## Exercise

Also send the column names to the template and display them as an HTML list.
