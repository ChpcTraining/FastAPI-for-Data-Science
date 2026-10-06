# Final Project — CSV Data Viewer & Plotter

## Objective

Build a complete FastAPI data-science web application.

The user should be able to:

1. Upload a CSV.
2. See the filename.
3. See the number of rows.
4. See the number of columns.
5. See column names.
6. Preview the first 20 rows.
7. View descriptive statistics.
8. Choose columns for visualisation.
9. Choose a plot type.
10. Generate and display a plot.

## Suggested interface

```text
--------------------------------------------

             CSV DATA EXPLORER

            [ Choose File ]
               [ Analyse ]

--------------------------------------------

Dataset: students.csv

Rows: 1000
Columns: 8

--------------------------------------------

DATA PREVIEW

| Name  | Age | Score |
|-------|-----|-------|
| Alice | 24  | 78    |
| Bob   | 27  | 85    |

--------------------------------------------

STATISTICAL SUMMARY

       count   mean   std   min   max
Age      ...
Score    ...

--------------------------------------------

CREATE VISUALISATION

X Column:  [ Age      ▼ ]
Y Column:  [ Score    ▼ ]
Plot Type: [ Scatter  ▼ ]

           [ Generate Plot ]

--------------------------------------------

                 PLOT

--------------------------------------------
```

## Suggested project structure

```text
fastapi-data-science/
├── main.py
├── requirements.txt
├── templates/
│   ├── upload.html
│   ├── results.html
│   └── plot.html
├── static/
│   ├── css/
│   │   └── style.css
│   └── plots/
└── data/
    └── students.csv
```

## requirements.txt

```text
fastapi
uvicorn
jinja2
python-multipart
pandas
matplotlib
```

## Minimum requirements

Your application must successfully:

- Accept `.csv` uploads
- Load the file with Pandas
- Show dataset dimensions
- Show column names
- Show a preview
- Show descriptive statistics
- Generate at least one plot

## Extension challenges

Once the basic application works, add:

- CSV file validation
- Friendly errors for invalid files
- Missing-value counts
- Column data types
- Histograms
- Scatter plots
- Line plots
- Bar charts
- X/Y column selection
- CSS styling
- A download-results feature
- A JSON API endpoint

Example API:

```text
POST /api/analyse
```

Example response:

```json
{
    "rows": 1000,
    "columns": 8,
    "numeric_columns": 5
}
```

## What you have learned

By completing the project you have worked with:

```text
HTML
  ↕
FastAPI
  ↕
Python
  ↕
Pandas
  ↕
Matplotlib
```

You have also learned the basic architecture behind a web application:

```text
Browser → Request → Route → Processing → Template/JSON → Response
```

This provides a foundation for larger FastAPI applications, REST APIs and later frameworks such as Django.
