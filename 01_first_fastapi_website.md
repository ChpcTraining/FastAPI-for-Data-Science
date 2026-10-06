# Lesson 1 — Your First FastAPI Website

## Goal

Create and run your first FastAPI application and understand routes.

## Setup

```bash
mkdir fastapi-data-science
cd fastapi-data-science
python -m venv venv
```

Activate the environment.

Linux/macOS:

```bash
source venv/bin/activate
```

Windows:

```bash
venv\Scripts\activate
```

Install FastAPI and Uvicorn:

```bash
pip install fastapi uvicorn
```

Create `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Welcome to Data Science with FastAPI"}
```

Run:

```bash
uvicorn main:app --reload
```

Visit `http://127.0.0.1:8000`.

## What is happening?

`app = FastAPI()` creates the application.

`@app.get("/")` tells FastAPI to respond to a GET request for `/`.

The `home()` function is called and its result is returned to the browser.

## Exercise

Create `/about` that returns:

```json
{
    "course": "Data Science",
    "technology": "FastAPI",
    "language": "Python"
}
```
