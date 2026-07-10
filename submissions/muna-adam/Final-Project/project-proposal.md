# Stroke Risk Prediction

## Certificate Name
**MAYMUN ADEN MOHAMED**


## Project Title
**Stroke Risk Prediction**

## Project Description

Stroke is one of the leading causes of death and long-term disability worldwide. Early identification of individuals who are at risk can significantly improve prevention and treatment outcomes.

This project develops a machine learning model that predicts whether a person is at risk of stroke based on medical symptoms and demographic information, including:

- Age
- Chest pain
- High blood pressure
- Dizziness
- Fatigue
- Irregular heartbeat
- Other clinically relevant indicators

The final deliverable is a **REST API** that accepts patient information as **JSON** and returns:

- Stroke risk prediction (**At Risk** or **Not At Risk**)
- Confidence probability score

This solution can be integrated into:

- Healthcare applications
- Clinical decision-support systems
- Medical dashboards

to assist healthcare professionals in making faster and more consistent preliminary risk assessments.

# Problem Type

## Primary Problem Type: Classification

The primary objective of this project is **Classification**, where the machine learning model predicts whether a patient is:

- **At Risk**
- **Not At Risk**

based on medical symptoms and demographic information.

## Additional Model: Regression

To further demonstrate machine learning capabilities, the project also includes a **Regression** model that estimates the patient's **Stroke Risk (%)**, providing a numerical assessment of the probability of stroke.

# 4. Dataset

## Dataset Source

**Kaggle – Stroke Risk Prediction Dataset**

**Link:**  
*https://www.kaggle.com/datasets/mahatiratusher/stroke-risk-prediction-dataset*

## Dataset Size

The dataset contains **70,000 rows** and **18 features (columns)**. It includes demographic information, medical history, symptoms, and other clinically relevant indicators used to train and evaluate machine learning models for stroke risk prediction.

## Target Variables

This project uses two target variables:

### Primary Target (Classification)

- **At Risk (Binary):** Predicts whether a person is at risk of stroke (`1`) or not at risk (`0`).

### Secondary Target (Regression)

- **Stroke Risk (%):** Predicts the estimated percentage probability of stroke occurrence (0–100%).


## Main Features

| Feature | Description |
|---------|-------------|
| Age | Age of the patient. Stroke risk generally increases with age. |
| Chest Pain | Whether the patient experiences chest pain (1 = Yes, 0 = No). |
| Shortness of Breath | Indicates breathing difficulty. |
| Irregular Heartbeat | Presence of abnormal heart rhythm. |
| Fatigue & Weakness | Indicates unusual fatigue or weakness. |
| Dizziness | Whether the patient experiences dizziness. |
| Swelling (Edema) | Presence of swelling in the body. |
| Pain in Neck/Jaw/Shoulder/Back | Pain in these areas, which may indicate cardiovascular issues. |
| Excessive Sweating | Indicates unusual sweating. |
| Persistent Cough | Whether the patient has a persistent cough. |
| Nausea/Vomiting | Presence of nausea or vomiting. |
| High Blood Pressure | Indicates whether the patient has hypertension. |
| Chest Discomfort (Activity) | Chest discomfort during physical activity. |
| Cold Hands/Feet | Indicates poor blood circulation. |
| Snoring/Sleep Apnea | Presence of sleep-related breathing disorders. |
| Anxiety/Feeling of Doom | Psychological symptom associated with cardiovascular events. |


# 5. Algorithms I Plan to Train

To identify the best-performing model, I will train and compare multiple machine learning algorithms. Since this project includes both **classification** (predicting whether a patient is at risk of stroke) and **regression** (predicting the stroke risk percentage), I will evaluate algorithms suitable for each task.


## Classification Algorithms

| # | Algorithm | Why It Fits |
|---|-----------|-------------|
| 1 | Logistic Regression | A strong baseline model for binary classification. It works well with this dataset because most input features are binary (0 = symptom absent, 1 = symptom present), making it easy to estimate the probability that a patient is at risk of stroke. |
| 2 | Random Forest Classifier | Stroke risk depends on combinations of multiple symptoms and age. Random Forest can capture these complex relationships and is less likely to overfit than a single decision tree. |
| 3 | Gradient Boosting Classifier | This algorithm is effective for structured medical datasets because it learns from previous prediction errors, making it a strong candidate for achieving high classification accuracy. |

## Regression Algorithms

| # | Algorithm | Why It Fits |
|---|-----------|-------------|
| 1 | Linear Regression | A simple baseline model for predicting the continuous target **Stroke Risk (%)**. It helps measure how each symptom and age contribute to the estimated stroke risk. |
| 2 | Random Forest Regressor | The relationship between medical symptoms and stroke risk is not always linear. Random Forest Regressor can model these complex patterns and often improves prediction accuracy. |
| 3 | Gradient Boosting Regressor | This algorithm builds a sequence of models that correct previous errors, making it highly effective for estimating stroke risk percentages from multiple medical features. |

# 6. Evaluation Plan

To compare the performance of all machine learning models, I will use different evaluation metrics based on the type of prediction task.

## Classification Evaluation

The classification models will be evaluated using the following metrics:

- **Accuracy** – Measures the overall percentage of correct predictions.
- **Precision** – Measures how many patients predicted as **"At Risk"** are actually at risk.
- **Recall** – Measures how many truly at-risk patients are correctly identified.
- **F1-Score** – Balances Precision and Recall, making it suitable for evaluating overall classification performance.
- **ROC-AUC** – Measures how well the model distinguishes between the two classes across different decision thresholds.

### Best Classification Model Selection

The best classification model will be selected based on the **F1-Score** because it provides a balanced measure of Precision and Recall. In healthcare applications, it is important to correctly identify patients who are at risk while also reducing false alarms.

## Regression Evaluation

The regression models will be evaluated using the following metrics:

- **Mean Absolute Error (MAE)** – Measures the average prediction error in percentage points.
- **Root Mean Squared Error (RMSE)** – Penalizes larger prediction errors more heavily than MAE.
- **R² Score** – Measures how well the model explains the variation in stroke risk percentage.

### Best Regression Model Selection

The best regression model will be selected based on the **highest R² Score** because it indicates how well the model explains the variation in the target variable. **MAE** and **RMSE** will also be considered to ensure that prediction errors remain low.

# 7. Deployment Sketch

## Deployment Method

This project will be deployed using **Streamlit**, which provides an interactive web interface for the machine learning models. Users will enter patient information through a simple form, and the application will instantly display the prediction results.

## User Input

The Streamlit application will allow users to enter the following information:

- Age
- Chest Pain
- Shortness of Breath
- Irregular Heartbeat
- Fatigue & Weakness
- Dizziness
- Swelling (Edema)
- Pain in Neck/Jaw/Shoulder/Back
- Excessive Sweating
- Persistent Cough
- Nausea/Vomiting
- High Blood Pressure
- Chest Discomfort (Activity)
- Cold Hands/Feet
- Snoring/Sleep Apnea
- Anxiety/Feeling of Doom

## Output

After clicking the **Predict** button, the application will display:

- **Stroke Risk Classification** (At Risk or Not At Risk)
- **Estimated Stroke Risk (%)**

The interface will be simple, user-friendly, and designed to help users quickly understand the prediction results.

# 8. Repository Plan

stroke-risk-prediction/
│
├── dataset/                   # Dataset-ka mashruuca (CSV)
│   └── stroke_data.csv
│
├── models/                    # Modellada la tababaray iyo scaler-ka
│   ├── classification_model.pkl
│   ├── regression_model.pkl
│   └── scaler.pkl
│
├── app.py                     # Main Streamlit application (UI, user input, model loading, prediction, and output)
│
├── README.md                  # Sharaxaadda mashruuca, sida loo isticmaalayo
│
├── project_paper.md           # warbixinta mashruuca
│
