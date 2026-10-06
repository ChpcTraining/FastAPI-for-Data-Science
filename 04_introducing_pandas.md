# Lesson 4 — Introducing Pandas

## Goal

Add Pandas to the project and create a small dataset.

Install Pandas:

```bash
pip install pandas
```

Create `data/students.csv`:

```csv
name,age,score
Alice,24,78
Bob,27,85
Carol,23,91
David,29,67
Emma,25,88
```

Project:

```text
fastapi-data-science/
├── main.py
├── data/
│   └── students.csv
└── templates/
    └── index.html
```

Import Pandas:

```python
import pandas as pd
```

Pandas uses a `DataFrame` to represent tabular data.
