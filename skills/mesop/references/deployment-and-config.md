# Deployment and Configuration

## Running Locally

1.  **Development**:
    ```bash
    mesop main.py
    ```
    Features: Hot reload, debug errors.

2.  **Configuration**:
    Use environment variables or `.env` file.
    ```bash
    MESOP_STATE_SESSION_BACKEND=memory mesop main.py
    ```

## Cloud Run Deployment

Mesop apps are containerized and run as HTTP services.

### Procfile
Required for standard Python buildpacks.
```
web: gunicorn --bind :8080 main:me
```
*Note: `main:me` assumes `main.py` and `import mesop as me`.*

### Containerization
Standard Dockerfile example:
```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "main:me"]
```

## Hugging Face Spaces

1.  Create Space (Docker SDK).
2.  Add `Dockerfile` (see above).
3.  Add `README.md` config:
    ```yaml
    ---
    title: My App
    sdk: docker
    app_port: 8080
    ---
    ```
4.  Update Security Policy in `main.py`:
    ```python
    @me.page(
      security_policy=me.SecurityPolicy(
        allowed_iframe_parents=["https://huggingface.co"]
      )
    )
    ```

## Security

### Security Policy
Configure CSP and iframe permissions per page.
```python
@me.page(
  security_policy=me.SecurityPolicy(
    allowed_iframe_parents=["https://google.com"],
    allowed_connect_srcs=["https://api.openai.com"],
    dangerously_disable_trusted_types=False
  )
)
```

### Static Assets
Serve assets securely from a local folder.
```bash
MESOP_STATIC_FOLDER=static mesop main.py
```
Access via `/static/filename.png`.

## State Session Backends

Configure where user state is stored via `MESOP_STATE_SESSION_BACKEND`:

1.  **memory** (Default): Fast, local RAM. Good for single instance. Requires session affinity for multiple replicas.
2.  **file**: Local disk. Good for persistence across restarts if disk persists.
3.  **firestore**: Google Cloud Firestore. Best for scalable, serverless deployment.
4.  **sql**: SQL database (Postgres, etc.). Good for standard relational storage.

## Integration

### WSGI Mounting
Mount Mesop onto Flask/FastAPI.
```python
from mesop.server.wsgi_app import create_wsgi_app
flask_app = Flask(__name__)
mesop_app = create_wsgi_app(debug_mode=False)
```
