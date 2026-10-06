# Lesson 10 — Receiving the Uploaded File

## Goal

Receive a browser file upload with FastAPI.

```python
from fastapi import FastAPI, Request, UploadFile, File
from fastapi.templating import Jinja2Templates

app = FastAPI()
templates = Jinja2Templates(directory="templates")

@app.get("/")
def home(request: Request):
    return templates.TemplateResponse(
        request=request,
        name="upload.html"
    )

@app.post("/upload")
async def upload_csv(
    request: Request,
    file: UploadFile = File(...)
):
    return {
        "filename": file.filename
    }
```

`UploadFile` represents the uploaded file.

The route uses POST because the browser is sending data to the server.

## Exercise

Return both the filename and its content type.
