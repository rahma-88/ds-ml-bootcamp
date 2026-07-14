# Final Project Proposal

**Date:** July 2026

---

## 1. Certificate Name

**Abdurahman Aden Mohamed**

---

## 2. Project Title and Description

**Title:** Crop Recommendation API

Farmers often decide what to plant based on habit or guesswork, even though soil nutrients and local weather conditions play a big role in whether a crop will actually thrive. This matters a lot in an economy like Ethiopia's, where agriculture is a major source of income and food security depends on getting these decisions right. This project builds a model that takes a few measurable inputs, soil nitrogen, phosphorus, and potassium levels, along with temperature, humidity, rainfall, and pH, and recommends the crop best suited to those conditions. An extension officer, a cooperative, or even a farmer with a soil test kit could use this to make a more informed planting decision instead of relying on guesswork.

---

## 3. Problem Type

**Classification**: this is a multi-class problem. Given a set of soil and climate readings, the model picks one crop out of 22 possible options as its recommendation.

This is supervised learning. Each row in the dataset already has a known best-fit crop label, so the model learns the relationship between conditions and crop from those examples.

---

## 4. Dataset

- **Source:** [Crop Recommendation Dataset](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset) (Kaggle).
- **Size:** 2,200 rows, 8 columns. The dataset is clean, with no missing values, and evenly balanced across all 22 crop classes (100 rows per crop).
- **Target column:** `label`, the recommended crop. There are 22 possible values, including rice, maize, chickpea, coffee, cotton, banana, mango, and others.
- **Main features:**
  - `N`: nitrogen content in the soil
  - `P`: phosphorus content in the soil
  - `K`: potassium content in the soil
  - `temperature`: average temperature in degrees Celsius
  - `humidity`: relative humidity as a percentage
  - `ph`: soil pH level
  - `rainfall`: rainfall in millimeters

**Preprocessing plan:** since the dataset has no missing values, preprocessing mainly means scaling the numeric features (all seven are numeric), encoding the `label` column for models that need numeric targets, and splitting into an 80/20 train/test set, stratified on `label` so every crop is represented proportionally in both sets.

---

## 5. Algorithms I Plan to Train

| # | Algorithm | Why it fits |
| --- | --- | --- |
| 1 | **Logistic Regression (multinomial)** | Bootcamp baseline extended to multi-class. Gives a simple, interpretable starting point before trying more complex models. |
| 2 | **Random Forest** | Bootcamp ensemble method. Naturally handles multi-class problems and tends to perform well on this kind of dataset without much tuning. |
| 3 | **K-Nearest Neighbors (KNN)** | I'll research this one on my own. Since the classes are well separated by soil and climate values, a distance-based method like KNN is a reasonable candidate for strong performance here. |

That covers the minimum of three. Two come from the bootcamp lessons, and KNN is the one I'll dig into through the scikit-learn documentation. I may add Support Vector Machine or Gradient Boosting as a fourth if time allows.

---

## 6. Evaluation Plan

**Metrics for all three models, measured on the same held-out test set:**

- Accuracy
- Precision (weighted average across all 22 classes)
- Recall (weighted average across all 22 classes)
- F1-Score (weighted average across all 22 classes)
- Confusion Matrix

**Best-model rule:** I'll rank the models by **weighted F1-Score**. With 22 classes, a single wrong prediction can hurt one crop's precision or recall much more than another's, so a weighted average keeps the comparison fair across classes of equal size. Since the dataset is balanced, accuracy should track closely with F1 here, but F1 remains the primary rule in case any model performs unevenly across specific crops.

---

## 7. Deployment Sketch

- **Framework:** FastAPI.
- **Endpoint:** `POST /predict`
- **Input JSON example:**

```json
{
  "N": 90,
  "P": 42,
  "K": 43,
  "temperature": 20.87,
  "humidity": 82.0,
  "ph": 6.5,
  "rainfall": 202.9
}
```

- **Output JSON example:**

```json
{
  "prediction": "rice",
  "probability": 0.94
}
```

The API loads the winning model from `models/best_model.pkl`, along with the fitted scaler and label encoder, so incoming JSON gets preprocessed the same way the training data was, and the numeric prediction gets mapped back to a crop name before the response is sent.

---

## 8. Repository Plan

```
crop-recommendation-api/
├── dataset/
│   └── crop_recommendation.csv
├── src/
│   ├── preprocess.py      # scaling, label encoding, train/test split
│   └── train.py           # trains all three models, prints comparison table, saves best
├── api/
│   └── app.py              # FastAPI app with /predict
├── models/
│   ├── best_model.pkl
│   ├── scaler.pkl
│   └── label_encoder.pkl
├── README.md
├── requirements.txt
└── project_paper.md
```

**Planned run commands:**

```bash
python src/train.py
uvicorn api.app:app --reload
```

---
