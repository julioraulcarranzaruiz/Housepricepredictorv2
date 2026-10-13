## Intructions to build Container Image for this FastAPI App 

Create the Dockerfile in the root of the source code (`house-prcice-predictor`). 

Following is all the information you would need to start building the container image for this app 


  * Base Image : `python:3.11-slim`
  * To install dependencies: `pip install -r requirements.txt`
  * Port: `8000`
  * Launch Command : `uvicorn main:app --host 0.0.0.0 --port 8000`

Directory structure inside the container should look like this 

```
/app
  main.py
  schemas.py
  inference.py
  requirements.txt
  /models
     /trained
         house_price_model.pkl
         preprocessor.pkl
```

---

## Ejecutar la API en local (sin contenedor)

**Linux / macOS:**

```bash
cd house-price-predictor
source .venv/bin/activate
uvicorn src.api.main:app --reload --host 0.0.0.0 --port 8000
```

**Windows (PowerShell):**

```powershell
cd house-price-predictor
.\.venv\Scripts\Activate.ps1
uvicorn src.api.main:app --reload --host 0.0.0.0 --port 8000
```

Documentación interactiva: <http://localhost:8000/docs>

## Construir y ejecutar la imagen

```bash
# Mismo comando en Windows y Linux
docker build -t house-price-api:latest -f src/api/Dockerfile .
docker run --rm -p 8000:8000 house-price-api:latest
```

Montar los modelos entrenados desde el host:

```bash
# Linux / macOS
docker run --rm -p 8000:8000 -v "$(pwd)/models:/app/models" house-price-api:latest
```

```powershell
# Windows PowerShell
docker run --rm -p 8000:8000 -v "${PWD}\models:/app/models" house-price-api:latest
```

