# ModelX Optimization Sprint: Dementia Prediction (Non-Medical)

### Team Name: [Your Team Name Here]

## ?? Project Overview
This repository contains our solution for the **ModelX Optimization Sprint**. The challenge was to build a binary classification model to predict dementia risk using **strictly non-medical variables** (demographics, lifestyle, and social context).

Our final model achieves an accuracy of **67.31%**, representing a **15.27% improvement** over the random baseline.

---

## ?? Repository Structure
* **`FINAL_SUBMISSION.ipynb`**: **START HERE.** This is the self-contained final notebook. It performs the full pipeline (Data Cleaning ? Feature Engineering ? Ensemble Modeling) and outputs the final accuracy score.
* **`experiments/`**: Contains our developmental notebooks showing the iterative process:
    * `01_Data_Exploration.ipynb`: Initial cleaning and EDA.
    * `02_Baseline_Models.ipynb`: Logistic Regression and initial Random Forest trials.
    * `03_Optimization.ipynb`: Hyperparameter tuning and Gradient Boosting experiments.
* **`requirements.txt`**: List of Python dependencies required to run the code.

---

## ?? Methodology

### 1. Data Preprocessing
* **Filtering:** We rigorously excluded all medical/diagnostic variables (e.g., MMSE scores, CDR components) based on the Data Dictionary.
* **Handling Missing Data:** Instead of standard imputation, we recoded missing values (`-4`, `99`) to a unique identifier (`-1`). This allowed the model to utilize "missingness" as a predictive signal.
* **Encoding:** Categorical variables with ordinal bias (e.g., Visit Frequency) were One-Hot Encoded to prevent mathematical misinterpretation.

### 2. Feature Engineering
We engineered several features to capture "Cognitive Reserve" and social support:
* **`AGE_x_EDUC`**: An interaction term combining Age and Education. This became our **#1 most important predictor**, validating the hypothesis that education buffers cognitive decline.
* **Social Context:** We derived detailed binary indicators from caregiver data (Relationship, Co-residence status).

### 3. Model Architecture
We employed a **Soft Voting Ensemble (`VotingClassifier`)** combining two optimized models:
1.  **Random Forest:** To capture non-linear interactions and handle noisy data robustly.
2.  **Gradient Boosting:** To iteratively correct errors and reduce bias.

---

## ?? Results

| Model | Accuracy | Notes |
| :--- | :--- | :--- |
| **Baseline (Null Model)** | 52.04% | Guessing the majority class |
| Logistic Regression | 63.68% | High recall, but low precision |
| Random Forest (Base) | 66.42% | Good balance of precision/recall |
| **Ensemble (Final)** | **67.31%** | **Best Performance** |

---

## ?? How to Run
1. Clone the repository.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
