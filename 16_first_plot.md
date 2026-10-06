# Lesson 16 — Creating Your First Plot

## Goal

Create a plot from a DataFrame and show it on the website.

Example dataset:

```csv
name,age,score
Alice,24,78
Bob,27,85
Carol,23,91
David,29,67
Emma,25,88
```

Create a scatter plot:

```python
import matplotlib.pyplot as plt

plt.figure()
plt.scatter(df["age"], df["score"])
plt.xlabel("Age")
plt.ylabel("Score")
plt.title("Age vs Score")
plt.savefig("static/plots/plot.png")
plt.close()
```

Pass the plot path to the template:

```python
context={
    "plot": "plots/plot.png"
}
```

HTML:

```html
<img src="/static/{{ plot }}" alt="Dataset plot">
```

## Important

Always call:

```python
plt.close()
```

after saving a plot so figures do not remain open on the server.
