# Lesson 19 — Creating a Data Science API

## Goal

So far, our FastAPI application has returned results as **HTML webpages**.

Now we will create an actual **API endpoint** that:

1. Accepts a CSV file
2. Loads it using Pandas
3. Calculates summary information
4. Returns the results as **JSON**

The important difference is:

```text
Website
Browser → FastAPI → Pandas → HTML → User

API
Application → FastAPI → Pandas → JSON → Application
```

---

## 19.1 Create a Simple API Endpoint

```python
@app.get("/api/status")
def api_status():
    return {
        "status": "running",
        "service": "Data Science API"
    }
```

Visit:

```text
http://127.0.0.1:8000/api/status
```

FastAPI returns:

```json
{
    "status": "running",
    "service": "Data Science API"
}
```

Instead of returning an HTML page, we return structured data as JSON.

---

## 19.2 Create a CSV Analysis API

Create:

```text
POST /api/analyse
```

```python
@app.post("/api/analyse")
async def analyse_csv(file: UploadFile = File(...)):
    df = pd.read_csv(file.file)

    return {
        "filename": file.filename,
        "rows": df.shape[0],
        "columns": df.shape[1]
    }
```

The flow is:

```text
CSV → FastAPI → Pandas → JSON
```

---

## 19.3 Test the API with FastAPI Docs

Start the application:

```bash
uvicorn main:app --reload
```

Visit:

```text
http://127.0.0.1:8000/docs
```

Find `POST /api/analyse`, click **Try it out**, select a CSV file and click **Execute**.

Example response:

```json
{
    "filename": "students.csv",
    "rows": 5,
    "columns": 3
}
```

---

## 19.4 Return Column Information

Pandas can give us the column names:

```python
columns = df.columns.tolist()
```

Update the endpoint:

```python
@app.post("/api/analyse")
async def analyse_csv(file: UploadFile = File(...)):
    df = pd.read_csv(file.file)

    return {
        "filename": file.filename,
        "rows": df.shape[0],
        "columns": df.shape[1],
        "column_names": df.columns.tolist()
    }
```

Example response:

```json
{
    "filename": "students.csv",
    "rows": 5,
    "columns": 3,
    "column_names": ["name", "age", "score"]
}
```

---

## 19.5 Return Summary Statistics

Pandas provides:

```python
df.describe()
```

Convert the result into a Python dictionary so it can be returned as JSON:

```python
summary = df.describe().to_dict()
```

Update the endpoint:

```python
@app.post("/api/analyse")
async def analyse_csv(file: UploadFile = File(...)):
    df = pd.read_csv(file.file)

    return {
        "filename": file.filename,
        "rows": df.shape[0],
        "columns": df.shape[1],
        "column_names": df.columns.tolist(),
        "summary": df.describe().to_dict()
    }
```

Example response:

```json
{
    "filename": "students.csv",
    "rows": 5,
    "columns": 3,
    "column_names": ["name", "age", "score"],
    "summary": {
        "age": {
            "count": 5,
            "mean": 25.6,
            "min": 23,
            "max": 29
        },
        "score": {
            "count": 5,
            "mean": 81.8,
            "min": 67,
            "max": 91
        }
    }
}
```

---

## 19.6 The Complete Endpoint

```python
@app.post("/api/analyse")
async def analyse_csv(file: UploadFile = File(...)):
    df = pd.read_csv(file.file)

    return {
        "filename": file.filename,
        "rows": df.shape[0],
        "columns": df.shape[1],
        "column_names": df.columns.tolist(),
        "summary": df.describe().to_dict()
    }
```

We have reused the same Pandas knowledge from the previous lessons and exposed it through an API.

---

## 19.7 Website vs API

A website route might return:

```python
return templates.TemplateResponse(...)
```

This produces **HTML**, primarily for people.

An API route might return:

```python
return {
    "rows": df.shape[0],
    "columns": df.shape[1]
}
```

This produces **JSON**, primarily for software.

```text
                    FastAPI
                       │
              ┌────────┴────────┐
              │                 │
           Website              API
              │                 │
            HTML               JSON
              │                 │
            Human          Application
```

---

## 19.8 Why Is This Useful?

We can write our Pandas analysis once and allow different applications to use it:

```text
Mobile App ───────┐
                  │
Website ──────────┼──→ FastAPI ──→ Pandas
                  │
Python Program ───┤
                  │
Research Tool ────┘
```

The API separates the **data processing functionality** from the user interface.

---

## 19.9 Test the API from Python

Install Requests:

```bash
pip install requests
```

Create `test_api.py`:

```python
import requests

url = "http://127.0.0.1:8000/api/analyse"

with open("students.csv", "rb") as file:
    response = requests.post(
        url,
        files={"file": file}
    )

print(response.json())
```

Run:

```bash
python test_api.py
```

The flow is now:

```text
test_api.py
     │
     │ POST students.csv
     ▼
FastAPI
     │
     ▼
Pandas
     │
     │ JSON
     ▼
test_api.py
```

---

## Exercise

Extend `/api/analyse` so that it also returns the number of missing values in each column.

Pandas provides:

```python
df.isnull().sum()
```

Convert it to a dictionary:

```python
df.isnull().sum().to_dict()
```

Your response should include something like:

```json
{
    "missing_values": {
        "name": 0,
        "age": 0,
        "score": 2
    }
}
```

---

## Final Challenge

Create another endpoint:

```text
POST /api/preview
```

It should accept a CSV and return the first five rows.

Hint:

```python
df.head().to_dict(orient="records")
```

Example response:

```json
[
    {
        "name": "Alice",
        "age": 24,
        "score": 78
    },
    {
        "name": "Bob",
        "age": 27,
        "score": 85
    }
]
```

---

## What You Have Learned

You now have both a **data science website and a data science API**:

```text
                  CSV DATA
                      │
                      ▼
                    Pandas
                      │
                      ▼
                   FastAPI
                  /       \
                 /         \
              HTML         JSON
               │             │
               ▼             ▼
             User       Other Software
```

This demonstrates one of FastAPI's main strengths for data science: the same Python and Pandas functionality can power both a human-facing website and an API that other software can consume.

---

[← Final Project](18_final_project.md) | [Course Home](index.md)
