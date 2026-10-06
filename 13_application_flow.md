# Lesson 13 — Understanding the Application Flow

## Goal

Understand how the pieces of the application work together.

```text
USER
  │
  │ GET /
  ▼
upload.html
  │
  │ select CSV
  ▼
POST /upload
  │
  ▼
FastAPI
  │
  ▼
Pandas
  │
  ├── read_csv()
  ├── head()
  ├── describe()
  └── shape
  │
  ▼
results.html
  │
  ▼
USER
```

## Compared with Streamlit

Streamlit might use:

```python
file = st.file_uploader("Upload CSV")
df = pd.read_csv(file)
st.dataframe(df)
```

FastAPI makes the web flow more explicit:

```text
Route → Request → Python processing → Response
```

This is a fundamental concept for building websites and APIs.
