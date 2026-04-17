# Architecture

## High-level flow

1. Read raw data from `notebook/data/stud.csv`
2. Save raw and split datasets into `artifacts/`
3. Transform features using a preprocessing pipeline
4. Train multiple regression models and select the best one
5. Save the chosen model and the preprocessing pipeline
6. Serve predictions using Flask and the saved artifacts

## Repository structure

- `app.py` — main Flask application for inference
- `requirements.txt` — Python packages needed to run the project
- `setup.py` — package metadata and install configuration
- `src/` — source code for ingestion, transformation, training, prediction, logging, and exceptions
  - `src/components/data_ingestion.py` — loads the original dataset and builds train/test splits
  - `src/components/data_transformation.py` — creates preprocessing pipelines and transforms data
  - `src/components/model_trainer.py` — trains, tunes, and selects regression models
  - `src/pipeline/predict_pipeline.py` — wraps loading the preprocessor/model and predicting on new records
  - `src/utils.py` — helper utilities for saving/loading objects and model evaluation
  - `src/logger.py` — logging configuration
  - `src/exception.py` — custom exception handling
- `artifacts/` — generated artifacts from training and preprocessing
  - `model.pkl` — trained model object
  - `preprocessor.pkl` — preprocessing pipeline object
  - `train.csv`, `test.csv`, `data.csv` — dataset artifacts
- `templates/` — HTML templates used by Flask
  - `index.html` — landing page
  - `home.html` — prediction form and result page

## Model artifacts

The Flask app depends on:

- `artifacts/preprocessor.pkl`
- `artifacts/model.pkl`

The pipeline loads both objects and applies preprocessing before prediction.

## Prediction process

- User submits values through the web form
- `CustomData` converts inputs into a `pandas.DataFrame`
- `PredictPipeline` loads serialized objects
- The data is transformed and passed to the trained model
- Predictions are returned to the UI
