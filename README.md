# Machine Learning Framework for Gas Hydrate Formation Temperature Prediction

## Overview

This repository contains the complete implementation of the research framework developed for predicting gas hydrate formation temperature using machine learning techniques.

The project covers the entire workflow, beginning with raw data preprocessing, followed by exploratory data analysis, standalone model development and optimization, and finally the implementation of stacked learning models with external validation.

The repository is organized to allow researchers to reproduce the study step-by-step.

---

# Repository Structure

The project is divided into the following notebooks.

## 1. Data Cleaning

-Prepare and clean the raw datasets before model development.
-For the composition dataset after cleaning added the two featured columns (reduced pressure and specific gravity)

Notebook

- 1 - Cleaning composition data.ipynb

---

## 2. Data Description

Explore the processed datasets and generate descriptive statistics and visualizations.

Notebook

- 2 - DATA DESCRIPTION.ipynb

---

## 3. Standalone Machine Learning Models

Develop, optimize, and evaluate individual machine learning models.

All saved models were trained using the final optimized pipeline with a leakage-aware validation strategy based on GroupKFold to prevent data leakage during hyperparameter optimization. The best hyperparameters obtained from this process were then used to retrain the final models, which are the saved models provided in this repository for external validation and inference.

Notebooks

- 3-1 SP_GR Dataset
- 3-2 Composition Dataset

---

## 4. Stacked Learning Models

Develop stacked learning frameworks using different combinations of base learners and meta-learners.

Notebooks

- 4-1-1 Stacked (SP_GR Dataset): XGBoost + Random Forest + ANN
- 4-1-2 Stacked (SP_GR Dataset): Random Forest + XGBoost + MLP
- 4-1-3 Stacked (SP_GR Dataset): GPR + XGBoost + MLP
- 4-2 Stacked (Composition Dataset): ANN + XGBoost + Random Forest

---

## Saved Models

The **SAVED MODELS** directory contains all pretrained models required for external validation.

Several notebooks load these models directly instead of retraining them.

---

# How to Run the Project

## Important Notes

1- Running the data cleaning or model training notebooks may overwrite the existing datasets and trained model files. If you need to preserve the original datasets or previously trained models, it is recommended to create backup copies before executing the notebooks.

2- After cleaning the Composition Dataset, two feature engineering variables—Pseudo-Reduced Pressure (Pr) and Specific Gravity (SP_GR)—were added. Consequently, all subsequent Jupyter notebooks should use the processed dataset composition_dataset_clean.csv rather than the dataset generated directly by the cleaning script.

3- Similarly, after cleaning the Specific Gravity Dataset, A small random perturbation with an average absolute variation of approximately 0.0016 was applied to the Specific Gravity values to reduce exact repetitions while preserving the original data distribution. Therefore, all Jupyter notebooks should use the processed dataset sp_gr_dataset_clean.csv instead of the dataset produced directly by the cleaning notebook.

For successful execution, please follow the steps below.

### Step 1

Download the repository.

---

### Step 2

Place all datasets in the same directory as the Jupyter notebooks.

Before running any notebook, verify whether the expected input file is:

- CSV
- Excel (.xlsx)

If necessary, convert the dataset to the required format.

---

### Step 3

1- For notebooks performing **external validation**, identify the required pretrained model from the notebook.

2- Copy the corresponding model from the **SAVED MODELS** folder into the same working directory as the notebook.

3- The external validation notebook supports flexible hybrid model configurations. Any standalone model can be excluded by commenting out (#) its prediction and corresponding meta-feature. The meta-learners will automatically use the remaining active models to generate the final hybrid predictions, allowing different ensemble combinations to be evaluated without changing the inference workflow.

4- The base models are saved to generate the first-level predictions, while the meta models are saved to combine these predictions into the final output. Saving both levels ensures that the same optimized models are reused during external validation, providing reproducible and consistent results without the need for retraining.
---

### Step 4

Execute the notebooks in the following order:

1. Cleaning Dataset
2. Data Description
3. Standalone Models
4. Stacked Models
5. External Validation

Running the notebooks sequentially ensures that all intermediate files required by subsequent notebooks are generated correctly.

---

# Requirements

The project was developed using:

- Python
- Jupyter Notebook

SYSTEM INFORMATION
============================================================
Operating System : Windows 10
Platform         : Windows-10-10.0.26200-SP0
Processor        : Intel64 Family 6 Model 186 Stepping 2, GenuineIntel
Python Version   : 3.10.4 (tags/v3.10.4:9d38120, Mar 23 2022, 23:13:41) [MSC v.1929 64 bit (AMD64)]

PACKAGE VERSIONS
============================================================
numpy           : 1.23.5
pandas          : 1.5.3
scipy           : 1.10.1
sklearn         : 1.2.2
matplotlib      : 3.10.8
joblib          : 1.5.3
xgboost         : 2.0.2
statsmodels     : 0.14.6
tensorflow      : 2.12.0
keras           : 2.12.0
torch           : Not Installed
openpyxl        : 3.1.5

To ensure reproducibility, it is strongly recommended to use the same Python package versions specified for this project. Running the notebooks with different library versions (e.g., TensorFlow, Keras, XGBoost, Scikit-learn, NumPy, or Pandas) may lead to differences in model behavior, training, or prediction results.

---

# Notes

- Some notebooks depend on outputs generated by previous notebooks.
- Do not rename datasets or pretrained model files unless the corresponding notebook is updated accordingly.
- Ensure that datasets and pretrained models are located in the notebook working directory before execution.
- If you retrain or save any models, avoid overwriting the existing saved models unless this is your intention. Instead, save the newly trained models using different filenames to preserve the original models and enable a direct comparison between the original and newly generated results.

