# Setup and Usage

## Prerequisites

- Python 3.8+ installed
- `pip` package manager
- Optional virtual environment tool such as `venv`

## Install dependencies

```bash
cd c:\Projects\ML-Project
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

## Run training manually

The training path is implemented through the `src/components/` modules. A simple way to execute the full training sequence is:

```bash
python -c "from src.components.data_ingestion import DataIngestion; from src.components.data_transformation import DataTransformation; from src.components.model_trainer import ModelTrainer; di=DataIngestion(); train_path,test_path=di.initiate_data_ingestion(); dt=DataTransformation(); train_arr,test_arr,_=dt.initiate_data_transformation(train_path,test_path); mt=ModelTrainer(); print(mt.initiate_model_trainer(train_arr,test_arr))"
```

This will create or update:

- `artifacts/data.csv`
- `artifacts/train.csv`
- `artifacts/test.csv`
- `artifacts/preprocessor.pkl`
- `artifacts/model.pkl`

## Start the Flask application

```bash
python app.py
```

Open a browser to:

- `http://127.0.0.1:5000/`

## Using the web UI

- Click the prediction page
- Enter student details and exam scores
- Submit the form to see the predicted math score

## Logging

Log files are generated under the `logs/` directory. Each run creates a timestamped `.log` file.

## Notes

- The web app requires the trained artifacts to exist before making predictions.
- If the model is missing, run the training sequence again.
- The repository includes a placeholder training pipeline file at `src/pipeline/training_pipeline.py`.
