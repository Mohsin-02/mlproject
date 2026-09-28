# Student Exam Performance Indicator

A machine learning project that predicts a student's maths score from their reading score, writing score, and selected background information. It includes data exploration, a training pipeline, model comparison, and a Flask web interface for making predictions.

## What the project does

A user enters:

- Gender
- Race or ethnicity group
- Parental level of education
- Lunch type
- Test preparation status
- Reading score
- Writing score

The application processes these inputs and displays a predicted maths score out of 100.

> This is a learning project. Its predictions should not be used to make decisions about individual students.

## Dataset and approach

The dataset contains **1,000 student records** and eight columns: seven input features and the target, `math_score`. The training pipeline uses an **80/20 train–test split** with `random_state=42`.

The preprocessing pipeline:

1. Fills missing numerical values with the median and standardizes numerical features.
2. Fills missing categorical values with the most frequent value, applies one-hot encoding, and scales the encoded features.
3. Fits preprocessing on the training data and applies the fitted transformation to the test data.

The training component compares Linear Regression, Decision Tree, Random Forest, Gradient Boosting, XGBoost, CatBoost, and AdaBoost regressors. It uses `GridSearchCV` for the parameter choices defined in the code, evaluates models with test-set R², and saves the selected model.

**Notebook result:** In the exploratory model-training notebook, Ridge Regression achieved the highest displayed test R² of approximately **0.881**. The notebook and the application's training pipeline evaluate different model sets, so this number should not be presented as the saved Flask model's verified score.

## Project structure

```text
ML-Project/
├── app.py                          # Flask routes and form handling
├── requirements.txt                # Python dependencies
├── setup.py                        # Package configuration
├── notebook/
│   ├── 1 . EDA STUDENT PERFORMANCE .ipynb
│   ├── 2. MODEL TRAINING.ipynb
│   └── data/stud.csv               # Source dataset
├── src/
│   ├── components/
│   │   ├── data_ingestion.py       # Loads and splits the data
│   │   ├── data_transformation.py  # Builds and saves preprocessing
│   │   └── model_trainer.py        # Compares and saves models
│   ├── pipeline/
│   │   └── predict_pipeline.py     # Loads artifacts and predicts
│   ├── utils.py                    # Model evaluation and serialization
│   ├── exception.py                # Custom exception handling
│   └── logger.py                   # Logging
├── templates/
│   ├── index.html                   # Landing page
│   └── home.html                    # Input form and prediction display
└── artifacts/                       # Generated datasets and model files


Student dataset
    → data_ingestion.py: save raw data and create train/test sets
    → data_transformation.py: fit preprocessing and transform both sets
    → model_trainer.py: tune, compare, and save a model
    → predict_pipeline.py: load saved preprocessing and model
    → app.py + home.html: collect inputs and show a prediction