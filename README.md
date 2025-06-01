# Hotel Reservation Prediction System

## Overview
This project implements a machine learning system to predict hotel reservation cancellations. It follows MLOps best practices with a complete pipeline from data ingestion to model deployment, including CI/CD integration with Jenkins and containerization with Docker.

## Project Structure
```
hotel_reservations/
├── artifacts/                  # Generated artifacts from the pipeline
│   ├── models/                 # Trained models
│   ├── processed/              # Processed datasets
│   └── raw/                    # Raw datasets
├── config/                     # Configuration files
│   ├── config.yaml             # Main configuration
│   ├── model_params.py         # Model hyperparameters
│   └── paths_config.py         # Path configurations
├── custom_jenkins/             # Custom Jenkins configurations
├── logs/                       # Application logs
├── mlruns/                     # MLflow experiment tracking
├── notebook/                   # Jupyter notebooks for exploration
├── pipeline/                   # Pipeline modules
│   └── training_pipeline.py    # Main training pipeline
├── src/                        # Source code
│   ├── custom_exception.py     # Custom exception handling
│   ├── data_ingestion.py       # Data ingestion from GCP
│   ├── data_preprocessing.py   # Data preprocessing
│   ├── logger.py               # Logging functionality
│   └── model_training.py       # Model training with LightGBM
├── static/                     # Static files for web app
├── templates/                  # HTML templates
│   └── index.html              # Main web interface
├── utils/                      # Utility functions
├── venv/                       # Virtual environment
├── application.py              # Flask web application
├── Dockerfile                  # Docker configuration
├── Jenkinsfile                 # Jenkins CI/CD pipeline
├── requirements.txt            # Project dependencies
└── setup.py                    # Package setup
```

## Features
- **Data Ingestion**: Fetches data from Google Cloud Storage and splits into training and test sets
- **Data Preprocessing**: 
  - Handles categorical variables with label encoding
  - Addresses data skewness
  - Performs feature selection using Random Forest importance
  - Handles class imbalance using SMOTE
- **Model Training**: 
  - Uses LightGBM classifier
  - Implements hyperparameter tuning with RandomizedSearchCV
  - Tracks experiments with MLflow
- **Model Deployment**: 
  - Flask web application for real-time predictions
  - Docker containerization
  - CI/CD pipeline with Jenkins
  - Deployment to Google Cloud Run

## Installation

### Prerequisites
- Python 3.x
- Google Cloud SDK
- Docker
- Jenkins (for CI/CD)

### Setup
1. Clone the repository:
   ```
   git clone https://github.com/naveenaddanki84/hotal_reservation_prediction_system.git
   cd hotal_reservation_prediction_system
   ```

2. Create and activate a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```
   pip install -e .
   ```

## Usage

### Running the Training Pipeline
To train the model:
```
python pipeline/training_pipeline.py
```

This will:
1. Download data from GCP bucket
2. Preprocess the data
3. Train a LightGBM model with hyperparameter tuning
4. Save the model and log metrics to MLflow

### Running the Web Application
To start the Flask application locally:
```
python application.py
```

The application will be available at http://localhost:8080

### Docker Deployment
Build and run the Docker container:
```
docker build -t hotel-reservation-prediction .
docker run -p 8080:8080 hotel-reservation-prediction
```

## CI/CD Pipeline
The project includes a Jenkinsfile that defines a CI/CD pipeline with the following stages:
1. Clone the repository
2. Set up the virtual environment and install dependencies
3. Build and push Docker image to Google Container Registry
4. Deploy to Google Cloud Run

## Model Details
- **Algorithm**: LightGBM Classifier
- **Features**: 
  - Lead time
  - Number of special requests
  - Average price per room
  - Arrival month and date
  - Market segment type
  - Number of week/weekend nights
  - Type of meal plan
  - Room type reserved
- **Evaluation Metrics**: Accuracy, Precision, Recall, F1 Score

## Configuration
The project uses YAML configuration files:
- `config/config.yaml`: Main configuration for data ingestion and processing
- `config/model_params.py`: Hyperparameter distributions for model tuning
- `config/paths_config.py`: File paths for artifacts

## Author
Naveen Addanki
