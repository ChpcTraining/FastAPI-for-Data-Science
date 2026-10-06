# Lesson 9 — Uploading a CSV

## Goal

Create an HTML form that lets the user choose a CSV file.

Install multipart support:

```bash
pip install python-multipart
```

Create `templates/upload.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>CSV Data Viewer</title>
</head>
<body>

<h1>CSV Data Viewer</h1>
<p>Upload a CSV file to analyse the dataset.</p>

<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="file" accept=".csv" required>
    <button type="submit">Analyse CSV</button>
</form>

</body>
</html>
```

The important attributes are:

```html
method="post"
enctype="multipart/form-data"
```

They allow the browser to send the selected file to the server.
