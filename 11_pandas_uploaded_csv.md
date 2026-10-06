# Lesson 11 — Reading Uploaded CSVs with Pandas

## Goal

Pass the uploaded file directly to Pandas.

```python
@app.post("/upload")
async def upload_csv(
    request: Request,
    file: UploadFile = File(...)
):
    df = pd.read_csv(file.file)

    rows = df.shape[0]
    columns = df.shape[1]

    return {
        "filename": file.filename,
        "rows": rows,
        "columns": columns
    }
```

The important line is:

```python
df = pd.read_csv(file.file)
```

Now the data does not have to be a fixed CSV already stored on the server.

## Exercise

Also return the list of column names:

```python
df.columns.tolist()
```
