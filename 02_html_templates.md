# Lesson 2 — Creating HTML Pages

## Goal

Use FastAPI to serve a normal HTML webpage.

Install Jinja2:

```bash
pip install jinja2
```

Create:

```text
fastapi-data-science/
├── main.py
└── templates/
    └── index.html
```

`templates/index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Data Science Portal</title>
</head>
<body>
    <h1>Data Science Portal</h1>
    <p>Welcome to my FastAPI website.</p>

    <h2>What can we do?</h2>
    <ul>
        <li>Upload datasets</li>
        <li>Analyse data</li>
        <li>View statistics</li>
        <li>Create plots</li>
    </ul>
</body>
</html>
```

Update `main.py`:

```python
from fastapi import FastAPI, Request
from fastapi.templating import Jinja2Templates

app = FastAPI()
templates = Jinja2Templates(directory="templates")

@app.get("/")
def home(request: Request):
    return templates.TemplateResponse(
        request=request,
        name="index.html"
    )
```

Run:

```bash
uvicorn main:app --reload
```

## Key concept

The flow is:

```text
Browser → FastAPI route → Python function → HTML template → Browser
```
