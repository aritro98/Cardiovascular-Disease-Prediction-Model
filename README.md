# Cardiovascular Disease Prediction Model

A predictive analytics solution that leverages machine learning to assess an individual’s risk of cardiovascular disease based on routine health measurements. By comparing multiple classification algorithms and combining them into a robust ensemble, this project delivers both high accuracy and actionable insights for early intervention.  

## Table of Contents
1. [Project Overview](#project-overview)
2. [Project Workflow](#project-workflow)
3. [Dataset Description](#dataset-description)
4. [Technologies Used](#technologies-used)
5. [Installation and Setup](#installation-and-setup)
6. [Usage](#usage)
7. [Results & Evaluation](#results-&-evaluation)
8. [Future Scope](#future-scope)

## Project Overview  
Predict the presence of cardiovascular disease using patient health metrics. We built, compared, and ensembled multiple ML models to achieve robust performance:

- **Logistic Regression**  
- **K-Nearest Neighbors (KNN)**  
- **Decision Tree**  
- **Random Forest**  
- **Naïve Bayes**  
- **Support Vector Machine (SVM)**  
- **CatBoost**  
- **Voting Ensemble**

The main workflow—including data cleaning, EDA, feature engineering, hyperparameter tuning, and final ensemble—is consolidated in `notebooks/Mini_Project.ipynb`.

## Project Workflow
1. **Data Cleaning & Preprocessing**
    - Handle missing values
    - Outlier removal
    - Feature scaling & encoding
2. **Exploratory Data Analysis**
    - Univariate & bivariate plots
    - Correlation heatmap
3. Model Training
    - Train 7 individual classifiers with cross-validation
    - Hyperparameter tuning via GridSearchCV
4. Ensemble Learning
    - Combine top-performing models in a VotingClassifier
    - Evaluate ensemble performance
5. Serialization
    - Save all the models to `models/`

All steps are executed in the merged notebook: `notebooks/Mini_Project.ipynb`.