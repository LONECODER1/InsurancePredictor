# Insurance Premium Predictor API

A production-ready machine learning REST API built with **FastAPI**, **Pydantic**, and **scikit-learn** that predicts insurance premium categories (`Low`, `Medium`, `High`) based on applicant profiles.

---

## Features

- **Machine Learning Inference**: Pre-trained model predicting risk categories with confidence score and probability distributions.
- **Input Validation**: Robust Pydantic v2 schemas validating age, BMI, lifestyle risks, and city tiers.
- **Dockerized**: Fully containerized with multi-stage layer caching and healthcheck endpoints.
- **Interactive Documentation**: Auto-generated Swagger UI and ReDoc endpoints.

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | API welcome message |
| `GET` | `/health` | Healthcheck and model status |
| `POST` | `/predict` | Predict insurance premium category |
| `GET` | `/docs` | Interactive Swagger UI |
| `GET` | `/redoc` | Interactive ReDoc documentation |

### Example Request (`POST /predict`)

```json
{
  "age": 28,
  "weight": 70.0,
  "height": 1.75,
  "income_lpa": 12.0,
  "smoker": false,
  "city": "Mumbai",
  "occupation": "private_job"
}
```

### Example Response

```json
{
  "response": {
    "predicted_category": "Low",
    "confidence": 0.74,
    "class_probabilities": {
      "High": 0.01,
      "Low": 0.74,
      "Medium": 0.25
    }
  }
}
```

---

## Quick Start with Docker

### Option A: Pull from Docker Hub
```bash
docker run -d -p 8000:8000 --name insurance-api adityagupta1112004/insurance-predictor:latest
```

### Option B: Build and Run Locally
```bash
# Build image
docker build -t insurance-predictor:latest -f DockerFile .

# Run container
docker run -d -p 8000:8000 --name insurance-api insurance-predictor:latest
```

### Option C: Using Docker Compose
```bash
docker compose up -d
```

Once running, visit **[http://localhost:8000/docs](http://localhost:8000/docs)** to test the API.

---

## Local Development (Without Docker)

1. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   # Windows:
   .\venv\Scripts\activate
   # Linux/macOS:
   source venv/bin/activate
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the development server:
   ```bash
   uvicorn app:app --reload --host 0.0.0.0 --port 8000
   ```
