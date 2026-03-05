# 📖 Insurance Premium Prediction API Documentation

This document provides detailed information about the API endpoints, request formats, and response structures.

## **Base URL**
When running locally with Docker: `http://localhost:8000`

---

## **1. Home Endpoint**
Returns a simple welcome message to verify the API is reachable.

- **URL:** `/`
- **Method:** `GET`
- **Description:** Basic connectivity check.
- **Success Response:**
  - **Code:** 200 OK
  - **Content:**
    ```json
    {
      "message": "Insurance Premium Prediction API"
    }
    ```

---

## **2. Health Check**
Checks the status of the API and ensures the machine learning model is loaded.

- **URL:** `/health`
- **Method:** `GET`
- **Description:** System health and model status.
- **Success Response:**
  - **Code:** 200 OK
  - **Content:**
    ```json
    {
      "status": "OK",
      "version": "1.0.0",
      "model_loaded": true
    }
    ```

---

## **3. Predict Premium**
The main endpoint used to predict the insurance premium category for a user.

- **URL:** `/predict`
- **Method:** `POST`
- **Description:** Predicts the premium category (e.g., Low, Medium, High) based on user demographics and health data.
- **Request Headers:** `Content-Type: application/json`

### **Request Payload (Sample)**
All fields are required.

```json
{
  "age": 35,
  "weight": 82.5,
  "height": 1.78,
  "income_lpa": 12.5,
  "smoker": true,
  "city": "Mumbai",
  "occupation": "private_job"
}
```

#### **Payload Field Details:**
| Field | Type | Description | Constraints |
| :--- | :--- | :--- | :--- |
| `age` | Integer | User's age | 1 to 119 |
| `weight` | Float | Weight in Kilograms | > 0 |
| `height` | Float | Height in Meters | 0.1 to 2.49 |
| `income_lpa` | Float | Annual Income (Lakhs Per Annum) | > 0 |
| `smoker` | Boolean | Smoking status | `true` or `false` |
| `city` | String | City of residence | e.g., "Delhi", "Pune" |
| `occupation` | String | User's job category | Must be one of the allowed literals* |

*\*Allowed Occupations: `retired`, `freelancer`, `student`, `government_job`, `buisness_owner`, `unemployed`, `private_job`.*

---

### **Response Structure (Sample)**
- **Success Response (200 OK):**
```json
{
  "predicted_category": "High",
  "confidence": 0.8942,
  "class_probabilities": {
    "Low": 0.0215,
    "Medium": 0.0843,
    "High": 0.8942
  }
}
```

- **Error Response (422 Unprocessable Entity):**
Occurs if the input data is missing or invalid (e.g., age is -5).
```json
{
  "detail": [
    {
      "loc": ["body", "age"],
      "msg": "ensure this value is greater than 0",
      "type": "value_error.number.not_gt"
    }
  ]
}
```

- **Error Response (500 Internal Server Error):**
Occurs if there is an issue with the model or prediction logic.
```json
{
  "error": "Error message details here..."
}
```

---

## **Interactive Documentation**
FastAPI automatically generates interactive documentation where you can test these endpoints directly:
- **Swagger UI:** [http://localhost:8000/docs](http://localhost:8000/docs)
- **ReDoc:** [http://localhost:8000/redoc](http://localhost:8000/redoc)
