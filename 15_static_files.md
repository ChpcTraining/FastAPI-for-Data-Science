# Lesson 15 — Serving Static Files

## Goal

Allow FastAPI to serve CSS, images and generated plots.

Import:

```python
from fastapi.staticfiles import StaticFiles
```

Mount the directory:

```python
app.mount(
    "/static",
    StaticFiles(directory="static"),
    name="static"
)
```

A file such as:

```text
static/plots/plot.png
```

can then be displayed at:

```text
/static/plots/plot.png
```

Static files are commonly used for:

- CSS
- JavaScript
- Images
- Generated plots
