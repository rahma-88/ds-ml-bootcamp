





# 1. Certificate Name:
**Hodan Maxamed Ibraahim**

# 2. Project Title and Description
Title:- **Crop Recommendation**

# Crop Recommendation 

Agriculture is one of the most important sectors for food production and economic development. However, many farmers struggle to select the most suitable crop because soil nutrients and weather conditions vary across different regions. Planting an unsuitable crop can result in low productivity, wasted resources, and financial losses. This project develops a Machine Learning-based Crop Recommendation  that predicts the most appropriate crop using soil and environmental factors such as Nitrogen (N), Phosphorus (P), Potassium (K), temperature, humidity, pH, and rainfall. By providing accurate crop recommendations, this project helps farmers make informed decisions, improve agricultural productivity, and promote efficient use of land and resources.


### 3. Problem Type

**Classification (Multi-Class Classification)**

The project predicts a crop category from **22 possible crop classes** such as **Rice, Maize, Cotton, Mango, Banana, and papaya** using soil and weather features such as N, P, K, temperature, humidity, pH, and rainfall.

 
### 4. Dataset

**Source:** Kaggle – Crop Recommendation Dataset
Link: https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset

**Size:** The dataset contains 2,200 rows and 8 columns.

**Target Column:**

* **label** – represents the recommended crop type (22 different crop classes).

**Main Features:**

* **N** – Nitrogen level in soil
* **P** – Phosphorus level in soil
* **K** – Potassium level in soil
* **temperature** – Temperature of the environment
* **humidity** – Humidity level
* **ph** – Soil pH value
* **rainfall** – Amount of rainfall



# 5. Algorithms I Plan to Train

1. **Random Forest Classifier** – It is suitable for multi-class classification and can handle different feature relationships to predict the best crop.

2. **Logistic Regression** – It provides a simple baseline model and works well for classification tasks with numerical features.

3. **XGBoost Classifier** – It is a powerful algorithm that can improve prediction accuracy by learning complex patterns in the data.


# 6. Evaluation Plan

**Metrics to compare models:**

* Accuracy
* Macro Precision
* Macro Recall
* Macro F1-score
* Confusion Matrix

**Best model selection metric:**
I will use **F1-score (Macro F1-score)** as the main metric to choose the best model. Since this is a multi-class classification problem with 22 crop classes, Macro F1-score gives equal importance to each class and provides a better evaluation of overall performance.


### 7. Deployment Sketch

**Framework:**
I will use **FastAPI** to deploy the machine learning model as a web API.

**/predict Endpoint Input (JSON fields):**

* N
* P
* K
* temperature
* humidity
* ph
* rainfall

**Example:**

```json
{
  "N": 90,
  "P": 42,
  "K": 43,
  "temperature": 25.6,
  "humidity": 80,
  "ph": 6.5,
  "rainfall": 200
}
```

**Output:**
The endpoint will return the predicted crop label and prediction probability.

Example:

```json
{
  "prediction": "Rice",
  "probability": 0.95
}
```


### 8. Repository Plan

```text
Crop-Recommendation-System/
│
├── data/
│   └── crop_recommendation.csv
│
├── notebooks/
│   └── crop_recommendation.ipynb
│
├── models/
│   └── crop_model.pkl
│
├── backend/
│   ├── app.py
│   
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
│
├── README.md
└── requirements.txt
└── .gitignore
```
