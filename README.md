# CardioGraph AI
## Explainable Cardiovascular Risk Prediction System

CardioGraph AI is an interactive machine learning system that predicts cardiovascular disease risk using patient health data. The system combines **XGBoost prediction**, **SHAP explainability**, and **interactive visualizations** to help users understand what factors contribute to heart disease risk and how lifestyle changes can reduce that risk.

This project was developed for the **Hack4Health – Byte 2 Beat Hackathon**, which focuses on building machine learning solutions using biomedical datasets to improve cardiovascular disease detection, understanding, and interpretability.

CardioGraph AI goes beyond simple prediction by integrating **explainable AI, lifestyle simulation, and risk factor visualization**, making the system easier to interpret and more useful for understanding cardiovascular health risks.

---

# Problem Statement

Cardiovascular disease (CVD) is the leading cause of death worldwide. Risk factors such as high blood pressure, elevated cholesterol, obesity, smoking, diabetes, and lack of physical activity significantly increase the likelihood of developing heart disease.

Although machine learning models can predict disease risk, many operate as **black boxes**, meaning users cannot easily understand the reasoning behind a prediction.

The goal of this project is to build a system that:

- Predicts cardiovascular disease risk using machine learning
- Explains which health factors influence the prediction
- Provides lifestyle recommendations to reduce risk
- Visualizes relationships between cardiovascular risk factors

This allows users to not only see their predicted risk but also understand **why the prediction was made and how they can reduce that risk**.

---

# Dataset

This project uses a **cardiovascular disease dataset containing approximately 70,000 patient records** with demographic, medical, and lifestyle indicators.

The dataset is de-identified and contains no personally identifiable information.

## Features

| Feature | Description |
|--------|-------------|
| age | Age of the patient |
| gender | Biological sex |
| height | Height of the patient |
| weight | Weight of the patient |
| BMI | Body Mass Index (derived feature) |
| ap_hi | Systolic blood pressure |
| ap_lo | Diastolic blood pressure |
| cholesterol | Cholesterol level |
| gluc | Glucose level |
| smoke | Smoking status |
| alco | Alcohol consumption |
| active | Physical activity level |

### Target Variable

```
cardio
0 = No cardiovascular disease
1 = Cardiovascular disease
```

---

# Feature Engineering

The dataset originally includes height and weight values. These are converted into **Body Mass Index (BMI)**, which is a more meaningful indicator of obesity-related cardiovascular risk.

BMI is calculated as:

```
BMI = weight / (height / 100)^2
```

BMI is widely used in medical research to evaluate obesity and cardiovascular risk.

---

# Machine Learning Model

The system uses **XGBoost (Extreme Gradient Boosting)**, a powerful ensemble learning algorithm designed for structured datasets.

XGBoost builds multiple decision trees sequentially and combines them to produce highly accurate predictions.

## Model Pipeline

```
Dataset
↓
Feature Engineering (BMI)
↓
StandardScaler Normalization
↓
Train/Test Split
↓
XGBoost Model Training
↓
Prediction
↓
Explainability with SHAP
```

---

# Model Evaluation

The model is evaluated using two standard classification metrics.

## Accuracy

Measures the proportion of correct predictions.

```
Accuracy = Correct Predictions / Total Predictions
```

## ROC-AUC Score

Measures how well the model distinguishes between patients with and without cardiovascular disease.

```
ROC-AUC closer to 1 → better classification
ROC-AUC closer to 0.5 → random guessing
```

Example model performance:

```
Model Accuracy: 0.73
Model ROC-AUC: 0.79
```

---

# Explainable AI (SHAP)

To make predictions interpretable, the system uses **SHAP (SHapley Additive Explanations)**.

SHAP calculates how much each feature contributes to the final prediction.

For each patient prediction the system shows:

- which features increase cardiovascular risk
- which features decrease cardiovascular risk
- the magnitude of each feature’s influence

Example explanation output:

```
Feature Impact on Prediction

Blood Pressure   +0.28
Cholesterol      +0.19
Smoking          +0.11
BMI              +0.07
Physical Activity -0.05
```

This helps users understand **why the model predicted a certain risk level**.

---

# Counterfactual Risk Simulation

The system also provides lifestyle improvement suggestions and recalculates the predicted risk after applying those changes.

Example:

```
Current Risk: 26.41%

Suggested Improvements
• Stop smoking
• Increase physical activity
• Reduce BMI

New Predicted Risk: 12.17%
```

This transforms the model into a **decision-support tool** that demonstrates how behavioral changes influence cardiovascular risk.

---

# Interactive Visualizations

CardioGraph AI includes two visualization systems to improve interpretability.

## Feature Impact Chart

An interactive **Plotly bar chart** visualizes how each feature contributes to the prediction.

Users can quickly identify the most influential health factors affecting cardiovascular risk.

## Risk Factor Network

A **NetworkX + PyVis graph** visualizes relationships between cardiovascular risk factors.

Example relationships:

```
Smoking → Blood Pressure → Heart Disease
Physical Activity → BMI → Blood Pressure
Cholesterol → Heart Disease
Alcohol → Heart Disease
```

### Node Colors

| Color | Meaning |
|------|---------|
| 🔴 Red | Major active risk factor |
| 🟠 Orange | Moderate risk |
| 🟢 Green | Protective factor |
| 🔵 Blue | Neutral factor |

This visualization helps users understand how different health variables interact and contribute to disease risk.

---

#  Application Architecture

```
User Health Input
↓
Data Preprocessing
↓
XGBoost Prediction
↓
Risk Probability
↓
SHAP Explanation
↓
Lifestyle Recommendations
↓
Interactive Visualizations
```

The entire system is deployed as an **interactive dashboard using Streamlit**.

---

# Technology Stack

### Programming Language
Python

### Machine Learning
- XGBoost
- Scikit-Learn

### Explainability
- SHAP

### Visualization
- Plotly
- PyVis
- NetworkX

### Data Processing
- Pandas
- NumPy

### Application Framework
- Streamlit

## Link to access this project
- https://cardioproj-ajvq7ncvb4h973nv6bwnyq.streamlit.app/
