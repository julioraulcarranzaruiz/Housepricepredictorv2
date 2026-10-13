## Instructions to build a Container Image 

  * Base Image : `python:3.9-slim`
  * Copy over everything in the build context (streamlit_app) path
  * Installing Dependencies : `pip install -r requirements.txt`
  * Port: 8501 
  * Launch Command : `streamlit run app.py --server.address=0.0.0.0`

---

## Ejecutar en local (sin contenedor)

**Linux / macOS:**

```bash
cd house-price-predictor
source .venv/bin/activate
pip install -r streamlit_app/requirements.txt
streamlit run streamlit_app/app.py
```

**Windows (PowerShell):**

```powershell
cd house-price-predictor
.\.venv\Scripts\Activate.ps1
pip install -r streamlit_app\requirements.txt
streamlit run streamlit_app\app.py
```

La interfaz queda en <http://localhost:8501>. Detén el servidor con `Ctrl + C`.

> Si la app llama a la API, define la URL antes de arrancar:
> `export API_URL=http://localhost:8000` (Linux) · `$env:API_URL="http://localhost:8000"` (Windows).
> Dentro de Docker Compose la URL es el nombre del servicio, por ejemplo `http://api:8000`.

## Construir y ejecutar la imagen

```bash
docker build -t house-price-ui:latest streamlit_app/
docker run --rm -p 8501:8501 house-price-ui:latest
```
