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

## Dataset Description
The dataset (`Cardiovascular_Disease_Dataset.csv`) contains the following columns:
| Column             | Type       | Range / Categories               | Description                                         |
|--------------------|------------|----------------------------------|-----------------------------------------------------|
| patientid          | integer    | 103,368 – 9,990,855              | Unique patient record identifier                    |
| age                | integer    | 20 – 80                          | Age in years                                        |
| gender             | categorical| 0 = female; 1 = male             | Patient gender                                      |
| chestpain          | categorical| 0, 1, 2, 3                      | Chest pain type (encoded)                           |
| restingBP          | integer    | 94 – 200 mm Hg                   | Resting blood pressure (systolic)                   |
| serumcholestrol    | integer    | 0 – 602 mg/dL                    | Serum cholesterol level                             |
| fastingbloodsugar  | binary     | 0 = ≤120 mg/dL; 1 = >120 mg/dL   | Fasting blood sugar indicator                       |
| restingrelectro    | categorical| 0, 1, 2                         | Resting electrocardiographic results (encoded)       |
| maxheartrate       | integer    | 71 – 202 beats/min               | Maximum heart rate achieved                         |
| exerciseangia      | binary     | 0 = no; 1 = yes                  | Exercise-induced angina                             |
| oldpeak            | float      | 0.0 – 6.2                        | ST depression induced by exercise relative to rest  |
| slope              | categorical| 0, 1, 2, 3                      | Slope of the peak exercise ST segment (encoded)      |
| noofmajorvessels   | categorical| 0, 1, 2, 3                      | Number of major vessels (0–3) colored by fluoroscopy|
| target             | binary     | 0 = no CVD; 1 = presence of CVD  | Diagnosis of cardiovascular disease (label)         |

## Technologies Used
- **Python** (≥ 3.8) – Core language for data processing & modeling
- **Pandas** – Data manipulation & analysis
- **NumPy** – Numerical computing
- **Scikit‑learn** – Model training, evaluation & preprocessing
- **CatBoost** – Gradient‑boosted decision trees for classification
- **Joblib** – Model serialization & deserialization
- **Matplotlib** – Plotting EDA visuals
- **Seaborn** – Statistical data visualization
- **Jupyter Notebook** – Interactive development environment

## Installation and Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/aritro98/Mini-Project-Cardiovascular-Disease-Prediction-Model.git
   ```
2. Navigate to the project directory:
   ```bash
   cd Mini-Project-Cardiovascular-Disease-Prediction-Model
   ```
3. Install the required Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage
1. Launch Jupyter Notebook
   ```bash
   jupyter notebook
   ```
   Open `notebooks/Mini_Project.ipynb` to run the full pipeline.
2. Load the saved models (For example: svm_CVD.pkl)
   ```python
   import joblib
   model = joblib.load("models/svm_CVD.pkl")
   ```
3. Prepare input data
Build a pandas DataFrame matching the model’s feature set (exclude `patientid` and `target`):
   ```python
   import pandas as pd
   sample = pd.DataFrame([{
       "age": 53,
       "gender": 1,
       "chestpain": 2,
       "restingBP": 120,
       "serumcholestrol": 158,
       "fastingbloodsugar": 0,
       "restingrelectro": 1,
       "maxheartrate": 147,
       "exerciseangia": 0,
       "oldpeak": 5.3,
       "slope": 3,
       "noofmajorvessels": 3
   }])
   ```
4. Make predictions
   ```python
   prediction = model.predict(sample)
   risk = "High risk of CVD" if prediction[0] == 1 else "Low risk of CVD"
   print(risk)
   ```

## Results & Evaluation
| Model                          | Accuracy | Precision | Recall | F1‑Score |
|--------------------------------|---------:|----------:|-------:|---------:|
| Logistic Regression            |     0.82 |      0.81 |   0.84 |     0.82 |
| K‑Nearest Neighbors            |     0.79 |      0.77 |   0.79 |     0.78 |
| Decision Tree                  |     0.75 |      0.73 |   0.76 |     0.74 |
| Random Forest                  |     0.85 |      0.84 |   0.86 |     0.85 |
| Naïve Bayes                    |     0.78 |      0.76 |   0.79 |     0.77 |
| Support Vector Machine (SVM)   |     0.83 |      0.82 |   0.84 |     0.83 |
| CatBoost                       |     0.86 |      0.85 |   0.87 |     0.86 |
| Ensemble Learning              |     0.88 |      0.87 |   0.89 |     0.88 |

## Future Scope
- **Deploy as a Web Service**: Containerize the model with Docker and serve via Flask/FastAPI or Streamlit for real‑time predictions.
- **Mobile Integration**: Build a mobile app (iOS/Android) that collects user vitals and returns CVD risk on the fly.
- **Extended Feature Engineering**: Incorporate additional biomarkers (e.g. cholesterol subtypes, C‑reactive protein) and lifestyle data (diet, sleep) to improve predictive power.
- **Deep Learning Models**: Experiment with neural architectures (e.g. feed‑forward, autoencoders) to capture non‑linear interactions.
- **Explainability & Fairness**: Integrate SHAP or LIME explanations, and audit model performance across demographic groups to ensure equity.
- **Continuous Learning Pipeline**: Set up an automated workflow (using Airflow or Kubeflow) to retrain the model as new patient data arrives.
- **Integration with EHR Systems**: Connect predictions to Electronic Health Record platforms for seamless clinical decision support.