# Lesson 12 — Creating a Results Page

## Goal

Display uploaded dataset analysis as HTML.

Create `templates/results.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Dataset Results</title>
</head>
<body>

<h1>Dataset Analysis</h1>

<h2>{{ filename }}</h2>

<p>Rows: {{ rows }}</p>
<p>Columns: {{ columns }}</p>

<h2>Data Preview</h2>
{{ table | safe }}

<h2>Statistical Summary</h2>
{{ summary | safe }}

<p><a href="/">Upload another dataset</a></p>

</body>
</html>
```

Update the route:

```python
@app.post("/upload")
async def upload_csv(
    request: Request,
    file: UploadFile = File(...)
):
    df = pd.read_csv(file.file)

    rows = df.shape[0]
    columns = df.shape[1]
    table = df.head(20).to_html(index=False)
    summary = df.describe().to_html()

    return templates.TemplateResponse(
        request=request,
        name="results.html",
        context={
            "filename": file.filename,
            "rows": rows,
            "columns": columns,
            "table": table,
            "summary": summary
        }
    )
```
