# Project Overview

## Purpose

This repository implements an end-to-end machine learning solution to predict student performance on a math exam using demographic and academic features.

## Problem statement

Given student data such as:

- gender
- race/ethnicity
- parental level of education
- lunch type
- test preparation course status
- reading score
- writing score

The model predicts the students `math_score`.

## Data source

The input dataset is stored in `notebook/data/stud.csv` and includes both feature columns and the target column `math_score`.

## Primary goals

- Build a reproducible data ingestion process
- Apply preprocessing for numeric and categorical features
- Train and evaluate multiple regression models
- Persist the best model and preprocessing object
- Expose inference through a Flask web interface

## What makes this project complete

- Modular structure in `src/`
- Model persistence in `artifacts/`
- Reusable inference pipeline in `src/pipeline/predict_pipeline.py`
- Flask UI for entering feature values and returning predictions
