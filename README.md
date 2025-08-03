# Return Risk Prediction for Womenswear in the UK
## Project Overview
This project aims to build and evaluate machine learning models to predict the return risk of women's apparel sold in the UK market. The primary goal is to classify products into three risk categories—'Low', 'Medium', and 'High'—to help retailers and brands proactively manage inventory, reduce costs associated with returns, and improve customer satisfaction.

The project simulates a real-world scenario by processing a dataset of product information, including textual descriptions, pricing details, and categorical attributes. The solution develops a robust classification pipeline that combines text-based features (using TF-IDF) with structured data and evaluates several machine learning models, including Logistic Regression, Random Forest, and XGBoost. The final, tuned models are saved for future use and deployment.

### Key Features
Data Cleaning and Preprocessing: Handles missing values, converts data types, and standardizes categorical and numerical features.

Feature Engineering: Combines product name, description, and care information into a single text feature, which is then vectorized using TF-IDF.

Simulated Target Variable: Creates a return_risk target variable based on a set of business rules to demonstrate a full end-to-end classification workflow.

Model Training and Evaluation: Compares the performance of three popular classification algorithms: Logistic Regression, Random Forest, and XGBoost.

Hyperparameter Tuning: Uses RandomizedSearchCV to optimize the performance of the Random Forest and XGBoost models.

Pipeline Implementation: Utilizes scikit-learn pipelines and ColumnTransformer to ensure a clean, reproducible, and efficient workflow.

Model Persistence: Saves the final, best-performing models to disk for easy deployment and future inference.

## Getting Started
### Prerequisites
To run this notebook, you will need to have Python 3.6+ installed along with the following libraries. You can install them using pip:

Bash

< pip install pandas scikit-learn numpy xgboost nltk joblib >
### Files and Directories
The project structure is organized as follows:


- data/raw/: Contains the original raw training and test datasets.

- data/stimulated_risk/: Stores the datasets with the newly created return_risk target variable after the cleaning and feature engineering steps.

- trained_models/: The directory where the trained machine learning models are saved.

- predict_risk_womensuk.ipynb: The main Jupyter Notebook that contains all the code for data processing, model training, and evaluation.

- README.md: This file.

### How to Run
1. Clone the repository or download the files.

2. Place the raw data files (training_data_womensUK.csv and test_data_womensUK.csv) into the data/raw/ directory.

3. Open the Jupyter Notebook: Launch Jupyter Notebook and open predict_risk_womensuk.ipynb.

4. Execute the cells sequentially: Run all the cells in the notebook from top to bottom. The notebook is designed to be self-contained and will create the necessary output directories and files.

## Project Methodology
1. Data Loading and Cleaning
The process begins by loading the training_data_womensUK.csv and test_data_womensUK.csv files. The data cleaning function addresses several issues, including:

- Standardizing column names.

- Handling missing values in categorical and numerical columns.

- Cleaning and converting currency and percentage strings to numerical types.

- Filling missing text data to prevent errors during vectorization.

2. Feature Engineering & Target Creation
- Text Vectorization: The Name, Description, and Care information columns are concatenated into a single text feature. A TfidfVectorizer is then used to convert this text into a numerical matrix, capturing the importance of different words.

- Target Variable (Simulated): A custom function, assign_return_risk, is used to create the target variable. This function applies a set of heuristic rules based on product attributes like Category, Full Price ($), and keywords in the product name. This approach serves as a controlled simulation to demonstrate the machine learning pipeline. Note: In a real-world application, this target would be derived from actual return data to build a predictive model that generalizes to unseen data.

3. Model Building & Evaluation
A machine learning pipeline is constructed using ColumnTransformer to handle different data types (categorical, numerical, and text features) automatically. This ensures that all preprocessing steps are consistently applied to the data.

The following models are trained and evaluated on a hold-out validation set:

- Logistic Regression: A linear baseline model.

- Random Forest: An ensemble model known for its high performance and ability to handle complex feature interactions.

- XGBoost: A powerful gradient boosting algorithm that often achieves state-of-the-art results.

4. Hyperparameter Tuning & Final Model Selection
RandomizedSearchCV is used to find the optimal hyperparameters for the Random Forest and XGBoost models. The performance of the tuned models is then compared to the baseline models. The best-performing model is then selected for the final evaluation on the test dataset.

5. Final Evaluation
The final step is to use the best-tuned models to make predictions on the completely unseen test_data_womensUK.csv. This provides a final, unbiased assessment of the model's performance and its ability to generalize to new data.