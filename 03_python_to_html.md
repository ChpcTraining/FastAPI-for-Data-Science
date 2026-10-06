# Lesson 3 — Passing Python Data to HTML

## Goal

Pass values from Python into an HTML template.

Update the route:

```python
@app.get("/")
def home(request: Request):
    students = 120

    return templates.TemplateResponse(
        request=request,
        name="index.html",
        context={"students": students}
    )
```

In `index.html`:

```html
<h2>Students</h2>
<p>Students registered: {{ students }}</p>
```

Jinja replaces `{{ students }}` with the Python value.

## Exercise

Create:

```python
course = "Data Science"
students = 120
weeks = 2
```

Pass all three values to the template and display them.

## Key concept

```text
Python variables → context dictionary → Jinja template → HTML
```
