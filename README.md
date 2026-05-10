# 🎓 Student Performance Predictor

An end-to-end machine learning project that predicts a student's **math score** based on demographic and academic background features. The project covers the full ML lifecycle — from data ingestion and preprocessing, to model training, evaluation, and deployment via a Flask web application.

---

## 📌 Project Overview

This project uses the [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams) dataset to build a regression model that estimates a student's math exam score given:

- Gender
- Race/Ethnicity
- Parental level of education
- Lunch type (standard or free/reduced)
- Test preparation course completion
- Reading score
- Writing score

The trained model is served through a Flask web app and is deployable to **AWS Elastic Beanstalk**.

---

## 🗂️ Project Structure

```
ml-project/
├── .ebextensions/          # AWS Elastic Beanstalk configuration
├── catboost_info/          # CatBoost training logs
├── notebook/               # EDA and model experimentation notebooks
├── src/
│   ├── components/         # Data ingestion, transformation, and model training
│   ├── pipeline/           # Training and prediction pipelines
│   ├── exception.py        # Custom exception handling
│   ├── logger.py           # Logging setup
│   └── utils.py            # Utility functions (model saving, evaluation)
├── templates/
│   ├── index.html          # Landing page
│   └── home.html           # Prediction form and results page
├── application.py          # Flask application entry point
├── requirements.txt        # Python dependencies
├── setup.py                # Package setup
└── .gitignore
```

---

## 🧠 ML Pipeline

1. **Data Ingestion** — Loads the dataset and splits it into train/test sets.
2. **Data Transformation** — Applies preprocessing:
   - `StandardScaler` for numerical features (reading score, writing score)
   - `OneHotEncoder` for categorical features (gender, race, etc.)
3. **Model Training** — Trains and evaluates multiple regression models, selecting the best performer. Models tested include:
   - Random Forest
   - Decision Tree
   - Gradient Boosting
   - XGBoost
   - CatBoost
   - AdaBoost
   - Linear Regression
4. **Prediction Pipeline** — Loads the saved model and preprocessor to make inference on new data.

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/gritzoogil/ml-project.git
cd ml-project

# Install dependencies
pip install -r requirements.txt
```

### Running the App

```bash
python application.py
```

Then open your browser and go to `http://localhost:5000`.

---

## 🌐 Web Application

The Flask app exposes two routes:

| Route | Method | Description |
|---|---|---|
| `/` | GET | Landing page |
| `/predictdata` | GET / POST | Form to enter student details and get a predicted math score |

---

## 📦 Dependencies

| Package | Purpose |
|---|---|
| `flask` | Web framework |
| `numpy` | Numerical computation |
| `pandas` | Data manipulation |
| `scikit-learn` | Preprocessing and ML models |
| `xgboost` | Gradient boosting (CPU) |
| `catboost` | Gradient boosting |
| `dill` | Model serialization |

---

## ☁️ Deployment

This project is configured for deployment on **AWS Elastic Beanstalk** via the `.ebextensions/` directory. The entry point is `application.py`, which uses the standard `application` variable name required by Elastic Beanstalk.

To deploy:

1. Install the [EB CLI](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html)
2. Initialize and deploy:

```bash
eb init -p python-3.8 ml-project
eb create ml-project-env
eb deploy
```

---

## 📓 Notebooks

The `notebook/` directory contains Jupyter notebooks for exploratory data analysis (EDA) and model experimentation. These serve as the research foundation for the production pipeline in `src/`.

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
