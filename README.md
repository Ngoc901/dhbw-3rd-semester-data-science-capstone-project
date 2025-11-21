# Data Science Capstone Project
- Team Member: Petra, Atai, David ,Niki (Ngoc Lan Hua)

## Deliverables:
[Final Presentation](https://www.canva.com/design/DAG4qgE2TzE/L9af6slFETYldMCZB1zkQw/view?utm_content=DAG4qgE2TzE&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h72f89c18e4)

[DS-2024_DHBW Excel Worksheet](https://docs.google.com/spreadsheets/d/1nFS5yj9ZwFKOWzB3w8jf31sijztGX80rrlKKkB9f5Ws/edit?gid=0#gid=0)

[Final Paper](https://docs.google.com/document/d/1G9RVMxbKTJhoqnfkapjaiLBl5WXV5lsUEczfuj6cDW0/edit?usp=sharing)



# Student Success Predictor: An Early Warning System

**DHBW-TINFO24 Data Science Capstone Project**

**Authors:** Atai Mamytov, Petra Namuyiga, David Lehmann, Ngoc Lan Hua
**Date:** November 2025

-----

## 📖 Project Overview

This project aims to solve a critical problem in education: identifying at-risk students *before* they fail.

Using the **UCI Student Performance Dataset**, we built an **Early Warning System** using machine learning. Unlike traditional grade predictors, our system deliberately excludes mid-term grades (`G1` and `G2`) to prevent data leakage and ensure early detection. It relies solely on demographic, behavioral, and socio-economic data to flag students at risk of failing (`G3 < 10`).

Our analysis compares four models—Decision Tree, K-Nearest Neighbors (KNN), Random Forest, and XGBoost—and uses advanced interpretability techniques (SHAP) to uncover the root causes of academic risk.

-----

## 📂 Repository Structure

```
student-success-predictor/
├── data/
│   ├── student-mat.csv        # Original Math dataset (from UCI)
│   ├── student-por.csv        # Original Portuguese dataset (from UCI)
│   ├── train_processed.csv    # Preprocessed & SMOTE-balanced training data
│   └── test_processed.csv     # Preprocessed & Imbalanced test data
│
├── notebooks/
│   ├── 01_EDA.ipynb           # Exploratory Data Analysis & Initial insights
│   ├── 02_Preprocessing.ipynb # Cleaning, Encoding, Dropping G1/G2, SMOTE
│   ├── 03_Models_BakeOff.ipynb # Training & Comparison of all models (Champion: RF)
│   └── analysis.ipynb         # Additional visualizations (School gap, etc.)
│
├── visuals/                   # Folder containing generated plots (SHAP, ROC, etc.)
├── requirements.txt           # List of python dependencies
└── README.md                  # Project documentation
```

-----

## 🚀 Quick Start Guide

Follow these steps to clone the repository and reproduce our results.

### 1\. Clone the Repository

Open your terminal and run:

```bash
git clone https://github.com/YOUR_USERNAME/student-success-predictor.git
cd student-success-predictor
```

### 2\. Set Up the Environment

We recommend creating a virtual environment to avoid dependency conflicts.

**Using venv (Mac/Linux):**

```bash
python3 -m venv venv
source venv/bin/activate
```

**Using venv (Windows):**

```bash
python -m venv venv
.\venv\Scripts\activate
```

### 3\. Install Dependencies

Install all required Python libraries:

```bash
pip install -r requirements.txt
```

*(Note: This project uses `xgboost`, `shap`, and `imbalanced-learn` alongside standard data science libraries.)*

### 4\. Run the Notebooks

Launch Jupyter Lab or Notebook:

```bash
jupyter lab
```

We recommend running the notebooks in the following order:

1.  **`01_EDA.ipynb`**: To see our initial data exploration and the discovery of the "Data Leakage" problem.
2.  **`02_Preprocessing.ipynb`**: To see how we dropped `G1`/`G2` and applied SMOTE to balance the classes.
3.  **`03_Models_BakeOff.ipynb`**: **(Main Notebook)** Run this to train the models, see the comparison table, and generate the final SHAP plots.

-----

## 📊 Key Findings & Methodology

### The Challenge

  * **Imbalance:** Only 15.4% of students were "At-Risk."
  * **Leakage:** `G1` and `G2` were 90%+ correlated with the final grade, making early prediction impossible if included.

### The Strategy

  * **Preprocessing:** We removed `G1`/`G2` and applied **SMOTE** to the training set to create a perfectly balanced dataset (384 Pass / 384 Fail).
  * **Models Tested:** Decision Tree, KNN, Neural Network (MLP), Random Forest, and XGBoost.
  * **Optimization:** We used `GridSearchCV` to tune hyperparameters for our top contenders.

### The Results (Early Warning System)

| Model | Accuracy | F1-Score (At-Risk) | AUC |
| :--- | :--- | :--- | :--- |
| **Random Forest (Tuned)** | **83.1%** | **0.42** | **0.79** |
| K-Nearest Neighbors | 77.4% | 0.39 | 0.74 |
| XGBoost (Tuned) | 79.5% | 0.44 | 0.75 |
| Decision Tree | 75.4% | 0.27 | 0.56 |

**Champion Model:** The **Tuned Random Forest** was selected for its robustness, high accuracy, and superior precision compared to the Neural Network.

### The Insights (SHAP Analysis)

Using SHAP values, we discovered the true drivers of risk:

1.  **Past Failures (`failures`):** The \#1 predictor of future risk.
2.  **Systemic Factors (`school`):** A 22% pass-rate gap between urban and rural schools.
3.  **Home Environment (`Medu`):** Mother's education level is a critical safety net.

-----

## 📝 License

This project is for educational purposes as part of the DHBW-TINFO24 Data Science module. The dataset is sourced from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/student+performance).
