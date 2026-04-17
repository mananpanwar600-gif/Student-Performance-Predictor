# Model Training and Inference

## Data ingestion

- Source file: `notebook/data/stud.csv`
- `src/components/data_ingestion.py` reads the dataset and writes:
  - `artifacts/data.csv`
  - `artifacts/train.csv`
  - `artifacts/test.csv`
- The split uses `train_test_split(..., test_size=0.2, random_state=42)`

## Preprocessing

- Implemented in `src/components/data_transformation.py`
- Numeric columns:
  - `writing_score`
  - `reading_score`
- Categorical columns:
  - `gender`
  - `race_ethnicity`
  - `parental_level_of_education`
  - `lunch`
  - `test_preparation_course`
- Numeric pipeline:
  - `SimpleImputer(strategy='median')`
  - `StandardScaler()`
- Categorical pipeline:
  - `SimpleImputer(strategy='most_frequent')`
  - `OneHotEncoder(handle_unknown='ignore')`
- The full `ColumnTransformer` is saved to `artifacts/preprocessor.pkl`

## Model selection

- Implemented in `src/components/model_trainer.py`
- Candidate regressors:
  - `RandomForestRegressor`
  - `DecisionTreeRegressor`
  - `GradientBoostingRegressor`
  - `LinearRegression`
  - `KNeighborsRegressor`
  - `XGBRegressor`
  - `CatBoostRegressor`
  - `AdaBoostRegressor`
- Hyperparameter tuning is performed with `GridSearchCV(cv=3)` using the search spaces defined in the module.
- The best model is selected by the highest test R² score.
- The selected model is persisted as `artifacts/model.pkl`.

## Inference pipeline

- `src/pipeline/predict_pipeline.py` contains:
  - `CustomData` — converts web form inputs into a `pandas.DataFrame`
  - `PredictPipeline` — loads `model.pkl` and `preprocessor.pkl`
- The pipeline transforms the input features and returns prediction results.

## Flask application flow

- `app.py` serves the HTML pages and handles prediction requests.
- Prediction form fields are collected in `home.html`.
- Submitted values are converted into the appropriate numeric and categorical inputs.
- The output is displayed on the same page after prediction.

## Artifact dependencies

The Flask app requires:

- `artifacts/preprocessor.pkl`
- `artifacts/model.pkl`

If these files are missing, rerun the training pipeline before serving.
