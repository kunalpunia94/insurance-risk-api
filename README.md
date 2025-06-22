# Insurance Premium Prediction API

A production-ready machine learning API that predicts a user's insurance premium category (`Low`, `Medium`, `High`) based on lifestyle and demographic inputs. This end-to-end pipeline includes data preprocessing, model inference, FastAPI backend, Docker containerization, and AWS deployment.

---

## Demo

FastAPI app is live at:  
**[http://13.201.128.6:8000](http://13.201.128.6:8000)**

- Health check endpoint: [http://13.201.128.6:8000/health](http://13.201.128.6:8000/health)  
- Prediction endpoint: POST to `/predict` with JSON body (see example below)

---

## Features

- Trained classification model using scikit-learn (serialized as `.pkl`)
- FastAPI backend for serving predictions
- Typed request/response validation via Pydantic
- Feature engineering inside input schema (`BMI`, `age group`, `lifestyle risk`, `city tier`)
- Dockerized application
- Hosted on AWS EC2 using Docker
- Ready for CI/CD, streamlit frontend integration, or MLflow monitoring (manual for now)

---

## Model Overview

- **Model Type**: Classification  
- **Classes**: `Low`, `Medium`, `High` (insurance premium categories)  
- **Input Parameters**:
  - Age, Height, Weight, Income (in LPA)
  - City, Smoker status, Occupation

**Derived Features**:
- `BMI`, `Age Group`, `Lifestyle Risk`, `City Tier`

---

## Sample Input

```json
POST /predict
Content-Type: application/json

{
  "age": 35,
  "weight": 75.0,
  "height": 1.75,
  "income_lpa": 15.0,
  "smoker": false,
  "city": "Pune",
  "occupation": "private_job"
}
```

---

## Sample Output

```json
{
  "response": {
    "predicted_category": "High",
    "confidence": 0.8432,
    "class_probabilities": {
      "Low": 0.01,
      "Medium": 0.15,
      "High": 0.84
    }
  }
}
```

---

## Project Structure
<pre><code>```text . ├── app.py # FastAPI entrypoint ├── Dockerfile # Docker container setup ├── model/ │ └── model.pkl # Trained ML model ├── schema/ │ ├── user_input.py # Input model with derived fields │ └── prediction_response.py ├── model/ │ └── predict.py # Prediction logic ├── config/ │ └── city_tier.py # Tier 1 and 2 cities ├── requirements.txt # Python dependencies ``` </code></pre>

---

## Docker Setup
### Build Docker Image
```
docker build -t insurance-premium-api .
```

---

### Run Container
```
docker run -d -p 8000:8000 insurance-premium-api
```

---

### Alternatively, pull and run from Docker Hub
```
docker pull kunalpunia94/insurance-premium-api:latest
docker run -d -p 8000:8000 kunalpunia94/insurance-premium-api:latest
```

---

## AWS Deployment

- Deployed on AWS EC2 with Docker
- Security group open on port 8000 for public access
- IP Address: http://13.201.128.6:8000

---

## API Endpoints
| Method | Endpoint   | Description               |
|--------|------------|---------------------------|
| GET    | /          | Welcome message           |
| GET    | /health    | Health check + version    |
| POST   | /predict   | Predict insurance premium |

---

## Local Testing
```
uvicorn app:app --reload
```
Then navigate to http://127.0.0.1:8000/docs to test via Swagger UI.
