# Australia Rain Prediction - End-to-End ML Pipeline

This project is an end-to-end Machine Learning solution designed to predict whether it will rain tomorrow in Australia, based on historical weather data. It covers the entire lifecycle of a machine learning project, from data ingestion and preprocessing to model training, tracking, and deployment using a FastAPI application.

## 🚀 Features

- **Data Pipeline**: Modularized scripts for data ingestion (`src/data_ingestion.py`), preprocessing (`src/data_preprocessing.py`), and model training (`src/model_training.py`).
- **Experiment Tracking**: Integrated with **MLflow** for tracking model parameters, metrics, and artifacts.
- **REST API**: Serves predictions using a fast and asynchronous **FastAPI** backend.
- **Containerization**: Includes a `Dockerfile` for easy deployment across any environment.
- **Cloud Storage Integration**: Connects with **Google Cloud Storage (GCS)** for managing datasets and/or artifacts.
- **Custom Logging & Exception Handling**: Built-in modules to trace errors and debug efficiently (`src/logger.py`, `src/custom_exception.py`).

## 📊 Model Performance

The current primary model is built using an **XGBoost Classifier**. Based on the test set evaluation, it achieves the following performance metrics:
- **Test Accuracy**: ~82%
- **Precision (Weighted Avg)**: ~85%
- **Recall (Weighted Avg)**: ~82%
- **F1-Score (Weighted Avg)**: ~83%

## 🛠️ Tech Stack

- **Language**: Python 3.10
- **Machine Learning**: Scikit-Learn, XGBoost, Pandas, NumPy
- **Experiment Tracking**: MLflow
- **API Framework**: FastAPI, Uvicorn
- **Containerization**: Docker
- **Cloud Provider**: Google Cloud Platform (Storage)

## 📂 Project Structure

```text
.
├── Data/                   # Raw and processed data files
├── artifacts/              # Serialized model and encoders (.pkl)
├── config/                 # Configuration files for the pipeline
├── mlruns/                 # MLflow experiment tracking local directory
├── notebook/               # Jupyter notebooks for EDA and experimentation
├── pipeline/               # Orchestration of the ML pipelines
├── src/                    # Core source code modules
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── model_training.py
│   ├── logger.py
│   └── custom_exception.py
├── utils/                  # Utility functions
├── app.py                  # FastAPI application entry point
├── Dockerfile              # Docker image configuration
├── requirements.txt        # Python dependencies
└── ...
```

## ⚙️ Setup and Installation

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd Australia
```

### 2. Create a Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
```

### 3. Install Dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Google Cloud Setup (Optional)
If you are pulling data or models from GCS, make sure you set the path to your service account JSON key:
```bash
export GOOGLE_APPLICATION_CREDENTIALS="/path/to/your/singular-citron-xxx.json"
```

## 🏃‍♂️ Running the Application

Start the FastAPI development server:
```bash
python app.py
```
The API will be available at: `http://localhost:8080`
Interactive API Documentation (Swagger UI) is available at: `http://localhost:8080/docs`

## 🐳 Docker Deployment

To run the application inside a Docker container:

1. **Build the image**
```bash
docker build -t rain-prediction-app .
```

2. **Run the container**
```bash
docker run -p 8080:8080 rain-prediction-app
```

## 📡 API Endpoints

### `GET /`
Returns a welcome message indicating the API is running.

### `GET /health`
Health check endpoint.

### `POST /predict`
Endpoint to get rain prediction for tomorrow. 

**Example Request Body (JSON):**
```json
{
  "Date": "2023-10-25",
  "Location": "Sydney",
  "MinTemp": 15.5,
  "MaxTemp": 25.2,
  "Rainfall": 0.0,
  "Evaporation": 5.4,
  "Sunshine": 10.2,
  "WindGustDir": "NE",
  "WindGustSpeed": 35.0,
  "WindDir9am": "E",
  "WindDir3pm": "NE",
  "WindSpeed9am": 15.0,
  "WindSpeed3pm": 20.0,
  "Humidity9am": 65.0,
  "Humidity3pm": 45.0,
  "Pressure9am": 1018.5,
  "Pressure3pm": 1015.2,
  "Cloud9am": 2.0,
  "Cloud3pm": 3.0,
  "Temp9am": 18.0,
  "Temp3pm": 23.5,
  "RainToday": "No"
}
```

**Example Response:**
```json
{
  "RainTomorrow": "No"
}
```
