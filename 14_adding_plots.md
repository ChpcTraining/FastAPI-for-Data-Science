# Lesson 14 — Adding Plots

## Goal

Add Matplotlib to the application.

Install:

```bash
pip install matplotlib
```

Create:

```text
static/
└── plots/
```

Project structure:

```text
fastapi-data-science/
├── main.py
├── data/
├── static/
│   └── plots/
└── templates/
    ├── upload.html
    └── results.html
```

Import Matplotlib:

```python
import matplotlib.pyplot as plt
```

Matplotlib can generate an image which FastAPI can then serve to the browser.
