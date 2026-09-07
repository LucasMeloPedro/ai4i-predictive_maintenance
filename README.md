# Predictive Maintenance (AI4I)

## Project Overview

This project aims to develop a machine learning model capable of predicting machine failures based on operational conditions and sensor data.
The project is being developed as a practical application of Machine Learning in mechanical engineering, more specific to **Predictive Maintenance**, combining data analysis, feature engineering, classification models and techniques for handling imbalanced datasets.
The project is currently under development.

---

## Project Objective

The main objective is to predict if a machine will fail based on its operational conditions.
The project is structured into two main stages:

1. **Failure Prediction:**
    Predict whether a machine will experience a failure and estimate the probability of failure. Based on the estimated probability, categorize the machine's risk level as Low, Medium or High. The objective of this stage is to achieve a good balance between failure detection and avoiding unnecessary maintenance alerts.

2. **Failure Mode Prediction:**
    Identify the type of failure when a failure is predicted.

> **Current status:** Stage 1 is under development. Stage 2 has not started yet.

---

## Dataset

The project uses the AI4I 2020 Predictive Maintenance Dataset, a synthetic dataset designed for predictive maintenance applications and originally made available through the UCI Machine Learning Repository.

The dataset contains operational and sensor measurements related to industrial machines, including: Air and process temperature, Rotational speed, Torque, Tool wear, Machine type and Machine failure

The target variable is:
* "Machine failure" — indicates whether a machine failure occurred.

The dataset presents a significant class imbalance, with failures representing only a small proportion of the observations (around 3,5%). Therefore, class imbalance is an important consideration throughout the modeling process.

**Source**: https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset

---

## Exploratory Data Analysis

Exploratory Data Analysis was conducted to understand the dataset, identify relationships between variables, investigate the distribution of machine failures, and identify potential patterns associated with failures.

Some relevant observations include:
* Strong negative correlation between rotational speed and torque. (Expected by relation between torque and angular speed, considering a constant power - demonstrated ahead)
* Power was investigated as an additional feature derived from torque and rotational speed.
* Extreme values of rotational speed and torque were investigated because they have shown a pattern related to failures.


**Status:** Completed

---

## Feature Engineering

A new "Power [W]" feature was created based on torque and rotational speed:

`Power = Torque × Angular Speed`

where angular speed is derived from rotational speed in RPM.

The analysis indicated that extreme power values were associated with a relevant proportion of machine failures. Therefore, the feature was retained for the modeling stage.

**Status:** Completed

---

## Machine Learning Models

Several classification approaches are being investigated to determine which model provides the most appropriate balance between detecting failures and avoiding unnecessary failure alerts.

### Random Forest

A Random Forest classifier was initially developed as a baseline model.

The baseline model achieved:

* **Precision:** 96%
* **Recall:** 74%
* **F1-score:** 83%

The impact of "class_weight='balanced" and hyperparameter optimization using GridSearchCV was also investigated.

Threshold optimization was subsequently explored to improve the balance between Precision and Recall.

An initial analysis of the probabilities related to thresholds in the test set indicated a promising result around a threshold of 0.33:

* **Precision:** 80%
* **Recall:** 81%
* **F1-score:** 80%

However, this threshold was identified using the test set and therefore will not be considered the definitive result. A further threshold analysis using out-of-fold validation on the training dataset is still required.

**Status:** Under evaluation

---

### XGBoost

An XGBoost classifier was also evaluated.

Different approaches for handling class imbalance and optimizing the model were investigated, including:

* Baseline XGBoost
* "scale_pos_weight"
* GridSearchCV
* Classification threshold optimization

The best XGBoost configuration evaluated so far, in terms of balance between Precision and Recall, was XGBoost combined with "scale_pos_weight".

Results:

* **Precision:** 79%
* **Recall:** 78%
* **F1-score:** 79%

**Status:** Completed

---

## Class Imbalance

Class imbalance is a major characteristic of this dataset because machine failures represent only a small fraction of all observations.

Different strategies were investigated during the modeling process, including:

* "class_weight" for Random Forest
* "scale_pos_weight" for XGBoost
* Threshold optimization
* Hyperparameter optimization
* Oversampling and SMOTE for Random Forest

The impact of these approaches is being evaluated primarily through Precision, Recall, and F1-score - rather than Accuracy - precisely because of the imbalance in the target variable.

---

## Model Evaluation

Because the target variable is highly imbalanced, Accuracy is not considered sufficient to evaluate model performance.

The main evaluation metrics used in this project are:

* **Precision** — measures how many predicted failures were actual failures.
* **Recall** — measures how many actual failures were correctly detected.
* **F1-score** — provides a balance between Precision and Recall.

The project places particular importance on the trade-off between **Recall and Precision**, since a predictive maintenance system should detect failures while avoiding an excessive number of false alarms.

**Status:** Ongoing

---

## Technologies

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib
* Jupyter Notebook
* Git
* GitHub

---

## Project Structure

The project is being developed using Jupyter Notebook for the analysis and modeling workflow, with Git and GitHub used to maintain the development history and experiment versions.

The repository structure and documentation will be refined as the project progresses.

---

## Next Steps

The next planned steps are:

1. Perform out-of-fold validation for Random Forest threshold selection.
2. Evaluate the selected threshold once on the test dataset.
3. Compare the best Random Forest and XGBoost results.
4. Select the most appropriate model for the project.
5. Complete the conclusions for Stage 1.
6. Begin Stage 2 — failure mode prediction.
7. Finalize the project documentation.
