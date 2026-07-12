# 1. Certificate Name

[Fadumo Mohamed Omar]

---

# 2. Project Title and Description

## Title: Flight Delay Prediction System

Airlines operate thousands of flights every day, and flight delays create problems for passengers, airports, and airline companies. Delays can increase operational costs, reduce customer satisfaction, and affect flight schedules.

This project builds a machine learning classification model that predicts whether a flight will be delayed based on historical flight information such as airline, departure time, destination airport, distance, and other flight-related factors.

The final deliverable is a machine learning prediction system that receives flight details and returns a delay prediction with a probability score. This system can be useful for airline planning, passenger notification systems, and operational decision-making.

---

# 3. Problem Type

**Classification — binary output: Delayed or On-Time.**

The target column is **Delayed** (or a delay status column depending on the dataset).

This is supervised learning because the model is trained using historical flight records where the final outcome (delay or no delay) is already known.

Output:

* 1 = Delayed
* 0 = On-Time

---

# 4. Dataset

**Source:** Flight Delay Dataset from Kaggle.

**Size:** Depends on the selected dataset (usually thousands to millions of flight records).

**Target:**

* Flight delay status (Delayed / Not Delayed)

### Main Features:

* Airline — airline company name (categorical)
* Origin Airport — departure airport
* Destination Airport — arrival airport
* Scheduled Departure Time — planned departure time
* Actual Departure Time — real departure time
* Arrival Time — arrival information
* Distance — flight distance (numeric)
* Day of Week — travel day
* Month — flight month
* Weather conditions (if available)
* Flight Duration — total flight time

### Preprocessing Plan:

* Handle missing values
* Remove duplicate records
* Convert date/time features
* Extract useful features (hour, day, month)
* Encode categorical variables
* Scale numerical features
* Stratified train/test split (80/20)

---

# 5. Algorithms I Plan to Train

| # | Algorithm                    | Why it fits                                                                             |
| - | ---------------------------- | --------------------------------------------------------------------------------------- |
| 1 | Logistic Regression          | Strong baseline model for binary classification and easy interpretation.                |
| 2 | Random Forest Classifier     | Handles complex relationships, reduces overfitting, and works well with mixed features. |
| 3 | Gradient Boosting Classifier | Powerful ensemble algorithm that often performs well on structured datasets.            |

This meets the requirement of training at least three machine learning algorithms.

The first two models are based on classification methods learned during the bootcamp, while Gradient Boosting will be researched using scikit-learn documentation and tutorials.

---

# 6. Evaluation Plan

All models will be evaluated using the same test dataset.

Metrics:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix
* ROC-AUC Score

### Best Model Selection:

The final model will be selected based on the highest **F1-Score** because flight delay prediction requires balancing:

* Correctly identifying delayed flights (Recall)
* Avoiding unnecessary delay predictions (Precision)

If two models have similar F1-Scores, ROC-AUC and Recall will be considered.

The best model will be saved and used for deployment.

---

# 7. Deployment Sketch

**Framework:** FastAPI

FastAPI will be used to create a REST API that allows users to send flight information and receive delay predictions.

## Endpoint:

```
POST /predict
```

### Input JSON Example:

```json
{
  "Airline": "Delta",
  "Origin": "JFK",
  "Destination": "LAX",
  "Distance": 2475,
  "Departure_Hour": 14,
  "Day_of_Week": 5,
  "Month": 7
}
```

### Output JSON Example:

```json
{
  "prediction": "Delayed",
  "probability": 0.82
}
```

The API will load the saved best model from:

```
models/best_model.pkl
```

along with preprocessing files such as encoders and scalers.

---

# 8. Repository Plan

```
flight-delay-prediction/
│
├── dataset/
│   ├── raw_flights.csv
│   └── cleaned_flights.csv
│
├── src/
│   ├── preprocess.py
│   └── train.py
│
├── api/
│   └── app.py
│
├── models/
│   ├── best_model.pkl
│   ├── scaler.pkl
│   └── encoder.pkl
│
├── notebooks/
│   └── exploration.ipynb
│
├── images/
│   ├── delay_distribution.png
│   ├── confusion_matrix.png
│   └── feature_importance.png
│
├── README.md
├── requirements.txt
└── project_paper.md
```

---

# 9. Expected Outcome

The project will produce a machine learning model capable of predicting flight delays from historical flight information.

The system will help demonstrate how machine learning can solve real-world aviation problems by improving decision-making, reducing operational problems, and providing better passenger services.

---
