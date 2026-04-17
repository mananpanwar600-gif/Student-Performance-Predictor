# End-to-End ML Student Performance Predictor

A production-style machine learning project that trains and serves a student performance regression model through a Flask web app.

## What this project does

- Ingests student exam data from `notebook/data/stud.csv`
- Preprocesses numeric and categorical features
- Trains multiple regression models and selects the best one automatically
- Persists the model and preprocessing pipeline to `artifacts/`
- Serves predictions using a Flask application with a simple web form

## Key components

- `app.py` — Flask web application for inference
- `src/components/data_ingestion.py` — dataset loading and train/test split
- `src/components/data_transformation.py` — preprocessing and feature transformation
- `src/components/model_trainer.py` — model training, tuning, and saving
- `src/pipeline/predict_pipeline.py` — runtime prediction pipeline on new inputs
- `artifacts/` — persisted model, preprocessor, and dataset splits

## Quick start

1. Create a Python environment and install dependencies:

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

2. Train the model (from a Python shell or script):

```bash
python -c "from src.components.data_ingestion import DataIngestion; from src.components.data_transformation import DataTransformation; from src.components.model_trainer import ModelTrainer; di=DataIngestion(); train_path,test_path=di.initiate_data_ingestion(); dt=DataTransformation(); train_arr,test_arr,_=dt.initiate_data_transformation(train_path,test_path); mt=ModelTrainer(); print(mt.initiate_model_trainer(train_arr,test_arr))"
```

3. Run the web app:

```bash
python app.py
```

4. Open the browser at `http://127.0.0.1:5000/`

## Project documentation

- `docs/PROJECT_OVERVIEW.md` — project goals and dataset details
- `docs/ARCHITECTURE.md` — component architecture and file structure
- `docs/SETUP_AND_USAGE.md` — installation, training, and serving instructions
- `docs/MODEL_TRAINING_AND_INFERENCE.md` — model pipeline, preprocessing, and inference details

## Notes

- `artifacts/model.pkl` and `artifacts/preprocessor.pkl` are required by the Flask app for prediction.
- The current training pipeline scaffold at `src/pipeline/training_pipeline.py` exists as a placeholder.
- Logs are written to the `logs/` directory.

