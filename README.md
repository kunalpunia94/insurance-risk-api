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

