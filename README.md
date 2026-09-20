IDRA Capstone Project — Patient Length of Stay Prediction

Predictive Analytics for Healthcare: Forecasting Patient Length of Stay in Urban Hospitals Using Machine Learning

Status: Completed
Project Type: IDRA Data Science & AI Final Capstone
Task: Regression
Target: lengthofstay

1. Project Overview

This project develops a machine-learning workflow for predicting
patient length of stay (LOS) using patient characteristics,
medical-condition indicators, clinical measurements, admission
information, and hospital facility information.

The project follows an end-to-end data science workflow:

Data Understanding → Data Quality → Data Cleaning → Leakage Detection
→ EDA → Statistical Analysis → Feature Engineering → Model Development →
Model Evaluation → Findings → Recommendations

The target variable is lengthofstay, so this is treated as a
regression problem.

2. Problem Statement

The objective is to investigate whether information available at or
before the intended prediction point can be used to estimate the number
of days a patient will remain hospitalized.

A key requirement is to avoid variables that reveal the outcome after
the fact.

3. Dataset

Dataset: Healthcare — Patient Length of Stay

Property

Value

Rows

61,680

Original columns

28

Target

lengthofstay

Target range

1–17 days

Target mean

~4.00 days

Target median

4 days

Main variable groups

Administrative / patient variables - gender - rcount - facid -
eid

Medical-condition indicators - dialysisrenalendstage - asthma -
irondef - pneum - substancedependence -
psychologicaldisordermajor - depress - psychother -
fibrosisandother - malnutrition - hemo

Clinical measurements - hematocrit - neutrophils - sodium -
glucose - bloodureanitro - creatinine - bmi - pulse -
respiration

Date / outcome variables - vdate - discharged - lengthofstay

4. Target Leakage Detection

A critical relationship was identified during validation:

discharged - vdate = lengthofstay

Therefore, discharged directly reveals the target and would create
target leakage.

The modelling workflow excludes:

discharged  → post-outcome information
eid         → identifier
vdate       → raw date string

Admission-time features are derived from vdate, including:

admission year

admission month

admission day of week

admission quarter

This keeps the model focused on information available at or before the
intended prediction point.

5. Research Questions

What are the main characteristics and data-quality properties of the
dataset?

Which medical conditions and clinical measurements show the
strongest observed relationships with length of stay?

How does length of stay vary across admission-count categories and
hospital facilities?

How accurately can length of stay be predicted without
post-discharge leakage?

How well do the selected regression models generalize to unseen test
records?

6. Objectives

Assess dataset structure and quality.

Identify missing values, duplicates and potential outliers.

Explore the distribution of length of stay.

Analyze relationships between predictors and length of stay.

Compare facilities and admission-count categories.

Detect and prevent target leakage.

Engineer appropriate admission-time features.

Develop multiple regression models.

Evaluate MAE, MSE, RMSE and R².

Compare training and testing performance.

Present findings, limitations and future work.

7. Project Workflow

Raw Dataset
     ↓
Data Understanding
     ↓
Data Quality Assessment
     ↓
Leakage Detection
     ↓
Cleaning & Feature Engineering
     ↓
Exploratory Data Analysis
     ↓
Statistical Analysis
     ↓
Train/Test Split
     ↓
Preprocessing Pipeline
     ↓
Linear Regression
Decision Tree Regressor
Random Forest Regressor
     ↓
Model Evaluation
     ↓
Findings & Discussion
     ↓
Final Report

8. Exploratory Data Analysis

8.1 Target Distribution

The distribution of lengthofstay is examined to understand its range,
central tendency and overall shape.

8.2 Facility Comparison

Average and median length of stay are compared across facid.

8.3 Admission Count Category

Observed mean length of stay increases across the rcount categories:

Admission Count

Mean LOS

0

2.72

1

3.71

2

5.27

3

6.27

4

7.25

5+

8.29

These are observed associations and should not be interpreted as causal
effects.

8.4 Correlation Analysis

Some of the stronger observed correlations with lengthofstay are:

Variable

Correlation

psychologicaldisordermajor

0.281

hemo

0.218

irondef

0.194

psychother

0.194

malnutrition

0.171

dialysisrenalendstage

0.170

Correlation is exploratory and does not establish causation.

9. Machine Learning Models

Three regression models are evaluated:

Linear Regression

A baseline model for approximately linear relationships.

Decision Tree Regressor

Captures nonlinear relationships and feature interactions.

Random Forest Regressor

An ensemble of decision trees designed to capture more complex nonlinear
patterns.

10. Preprocessing

Numerical variables

Median imputation

Standard scaling

Categorical variables

Most-frequent imputation

One-hot encoding

The preprocessing is implemented using Pipeline and
ColumnTransformer so that transformations are learned within the
training workflow.

11. Model Evaluation

The models are evaluated using:

MAE: Mean Absolute Error

MSE: Mean Squared Error

RMSE: Root Mean Squared Error

R²: Coefficient of Determination

Training and test performance are also compared to examine
generalization.

Final Results

Model

Train MAE

Test MAE

Train RMSE

Test RMSE

Train R²

Test R²

Random Forest

0.192

0.418

0.321

0.680

0.982

0.916

Decision Tree

0.625

0.688

0.828

0.938

0.877

0.840

Linear Regression

0.879

0.866

1.150

1.137

0.763

0.764

Random Forest test metrics

MAE  = 0.418 days
MSE  = 0.462
RMSE = 0.680 days
R²   = 0.916

Among the evaluated models, Random Forest produced the strongest
held-out test performance.

12. Key Findings

Length of stay varies substantially across the dataset.

Admission-count categories show increasing observed average length
of stay.

Facility-level differences are visible in the exploratory analysis.

Several medical-condition indicators have positive observed
relationships with length of stay.

Clinical measurements provide additional predictive information.

discharged is direct target leakage and was excluded.

Tree-based models outperform the linear baseline in this experiment.

Random Forest achieves a test RMSE of 0.680 days and test R² of
0.916.

The difference between training and test performance indicates a
generalization gap.

13. Limitations

The dataset may not generalize to other hospitals or populations.

Some clinically relevant factors may not be present.

Correlation does not imply causation.

Facility differences may reflect patient mix or operational
differences.

Random Forest shows a training/test performance gap.

The models have not been externally validated.

This is an academic predictive analytics project, not a clinically
validated decision-support system.

14. Recommended Project Structure

IDRA_Capstone_Healthcare_LengthOfStay/
│
├── README.md
│
├── data/
│   ├── raw/
│   │   └── P_1_LengthOfStay(1).csv
│   └── processed/
│       └── modeling_dataset.csv
│
├── notebooks/
│   └── IDRA_Capstone_Healthcare_LengthOfStay_Final_Executed.ipynb
│
├── reports/
│   ├── IDRA_Capstone_Healthcare_LengthOfStay_FINAL.pdf
│   └── IDRA_Capstone_Healthcare_LengthOfStay_FINAL.docx
│
├── outputs/
│   ├── data_quality_report.csv
│   ├── descriptive_statistics.csv
│   ├── facility_summary.csv
│   ├── rcount_summary.csv
│   ├── target_correlations.csv
│   └── model_results.csv
│
├── documentation/
│   └── data_dictionary.csv
│
└── figures/
    ├── figure1_los_distribution.png
    ├── figure2_facility_los.png
    ├── figure3_rcount_los.png
    ├── figure4_correlation_heatmap.png
    ├── figure5_model_rmse.png
    ├── figure6_actual_vs_predicted.png
    └── figure7_residuals.png

15. Important Files

File

Purpose

README.md

Project documentation

IDRA_Capstone_Healthcare_LengthOfStay_Final_Executed.ipynb

Reproducible analysis

IDRA_Capstone_Healthcare_LengthOfStay_FINAL.pdf

Final report

IDRA_Capstone_Healthcare_LengthOfStay_FINAL.docx

Editable report

modeling_dataset.csv

Leakage-controlled modelling data

data_dictionary.csv

Variable descriptions

data_quality_report.csv

Data-quality results

descriptive_statistics.csv

Descriptive statistics

facility_summary.csv

Facility analysis

rcount_summary.csv

Admission-count analysis

target_correlations.csv

Target correlations

model_results.csv

Model evaluation results

16. Technologies Used

Python

Jupyter Notebook / Google Colab

Pandas

NumPy

Matplotlib

Seaborn

Scikit-learn

Machine Learning

Linear Regression

Decision Tree Regressor

Random Forest Regressor

17. Installation

pip install pandas numpy matplotlib seaborn scikit-learn jupyter

Launch Jupyter:

jupyter notebook

Then open:

notebooks/IDRA_Capstone_Healthcare_LengthOfStay_Final_Executed.ipynb

The notebook can also be executed in Google Colab.

18. Reproducibility

The project uses:

random_state = 42

and an:

80% training / 20% testing

split.

The notebook contains the complete workflow from data loading through
model evaluation and result export.

19. Future Work

Potential extensions include:

Hyperparameter tuning with cross-validation.

Testing additional ensemble and boosting algorithms.

Temporal validation using later admissions as an independent test set.

External validation on another hospital dataset.

Error analysis by length-of-stay range.

Subgroup performance analysis.

Feature importance and explainability using permutation importance or
SHAP.

Prediction uncertainty estimation.

Fairness and subgroup-specific error analysis.

Development of an API or dashboard after appropriate validation.

20. Final Deliverables

The project submission contains:

✓ Final PDF Report
✓ Executed Jupyter Notebook
✓ Leakage-Controlled Modeling Dataset
✓ Data Dictionary
✓ Analysis Output CSV Files
✓ Figures
✓ README.md

21. Author

Student Name: Chinta Prithvi

Institute:
National Institute Of Technology, Andhra Pradesh

Institute Roll No.: 423124

Enrollment No.: IDRA-2026-498821

Program: B.Tech — Computer Science and Engineering

Project: IDRA Data Science & AI Final Capstone Project

22. Project Status

Completed

The project provides a complete end-to-end machine-learning workflow
covering data quality assessment, leakage detection, exploratory
analysis, statistical analysis, feature engineering, regression
modelling, evaluation, findings, limitations and future work.
