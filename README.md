# House Price per Square Foot Prediction using Linear Regression

## Project Overview

This project builds a **Linear Regression model to predict house price per square foot** using property-related features from a Kaggle house price dataset.

The project includes data cleaning, preprocessing, categorical feature encoding, model training, evaluation using RMSE and R², residual analysis, sample predictions, and saving the trained model as a reusable artifact.

> **Note:** The target variable in this dataset is `Price (in rupees)`, which represents the **price per square foot**, not the total property price.

---

## Dataset

The dataset was obtained from Kaggle:

**House Price Dataset**
https://www.kaggle.com/datasets/juhibhojani/house-price

The notebook automatically downloads the dataset using the Kaggle public API, so the raw dataset does not need to be uploaded to this repository.

### Dataset Size

Original dataset:

* Rows: **187,531**
* Columns: **21**

Rows with missing or invalid target values were removed before training.

---

## Objective

The main objective is to develop a simple regression model that can estimate the **price per square foot of a property** based on available property characteristics.

---

## Features Used

The following features were used for prediction:

### Numerical Features

* `Carpet Area`
* `Floor`
* `Bathroom`
* `Balcony`

### Categorical Features

* `location`
* `Transaction`
* `Furnishing`
* `facing`
* `overlooking`
* `Ownership`

### Target Variable

* `Price (in rupees)`

---

## Features Excluded

Some columns were excluded during preprocessing for data quality, relevance, or leakage concerns.

* `Index` — identifier
* `Title` — free-text field
* `Description` — free-text field
* `Amount(in rupees)` — total property price and potentially too closely related to the target
* `Plot Area` — completely missing
* `Dimensions` — completely missing
* `Society` — high missingness and high cardinality
* `Super Area` — high missingness
* `Status` — contained only one unique value
* `Car Parking` — inconsistent/noisy values

---

## Data Preprocessing

The following preprocessing steps were performed:

1. Loaded the dataset using Pandas.
2. Inspected dataset shape, data types, missing values, and descriptive statistics.
3. Removed rows where the target value was missing.
4. Removed rows where the target value was zero or negative.
5. Extracted numerical values from text-based fields such as:

   * `500 sqft` → `500`
   * `10 out of 11` → `10`
6. Missing numerical values were handled using **median imputation**.
7. Missing categorical values were handled using **most-frequent imputation**.
8. Categorical variables were converted into numerical representations using **One-Hot Encoding**.
9. The dataset was divided into training and testing sets using an **80/20 split**.

---

## Model

The regression algorithm used in this project is:

**Linear Regression**

The model was implemented using `scikit-learn` and combined with a preprocessing pipeline containing numerical imputation, categorical imputation, and one-hot encoding.

### Train-Test Split

* Training set: **80%**
* Testing set: **20%**
* Random state: **42**

---

## Evaluation Metrics

The trained model was evaluated on the test set using:

### RMSE

**Root Mean Squared Error (RMSE)** measures the typical magnitude of prediction errors. Lower values indicate better performance.

### R²

**R² (R-squared)** measures how much of the variation in the target variable is explained by the model. Higher values indicate better explanatory performance.

### Results

| Metric |       Result |
| ------ | -----------: |
| RMSE   | **3,867.50** |
| R²     |   **0.3717** |

The Linear Regression model provides a useful baseline, although the R² score indicates that a substantial amount of variation in price per square foot is not captured by this simple linear model.

---

## Sample Predictions

Example predictions from the test set:

| Actual Price | Predicted Price | Absolute Error |
| -----------: | --------------: | -------------: |
|     2,228.00 |        6,107.25 |       3,879.25 |
|    11,538.00 |        7,406.42 |       4,131.58 |
|    17,333.00 |       11,188.46 |       6,144.54 |
|     5,566.00 |        7,527.16 |       1,961.16 |
|     9,722.00 |        8,964.49 |         757.51 |
|     5,455.00 |        8,704.02 |       3,249.02 |
|     4,343.00 |        4,955.38 |         612.38 |
|     5,104.00 |        7,706.15 |       2,602.15 |
|    20,435.00 |       13,741.43 |       6,693.57 |
|     5,246.00 |        6,080.42 |         834.42 |

---

## Evaluation Plots

### Residual Plot

The residual plot shows the difference between actual and predicted values and helps evaluate the model's prediction errors.

![Residual Plot](plots/residual_plot.png)

### Actual vs Predicted

This plot compares the actual price per square foot with the model's predicted price per square foot.

![Actual vs Predicted](plots/actual_vs_predicted.png)

---

## Saved Model

The trained model is saved as:

```text
models/house_price_linear_regression.pkl
```

The model was saved using `joblib`.

This allows the trained preprocessing pipeline and Linear Regression model to be reused without retraining from scratch.

---

## Repository Structure

```text
AME_6_Linear-Regression-House-Price-Prediction_byte/
│
├── notebook/
│   └── House_price.ipynb
│
├── models/
│   └── house_price_linear_regression.pkl
│
├── plots/
│   ├── residual_plot.png
│   └── actual_vs_predicted.png
│
├── results/
│   ├── evaluation_metrics.csv
│   └── sample_predictions.csv
│
├── README.md
└── requirements.txt
```

---

## How to Reproduce the Project

### 1. Clone the repository

```bash
git clone https://github.com/NishatLuba/AME_6_Linear-Regression-House-Price-Prediction_byte.git
cd AME_6_Linear-Regression-House-Price-Prediction_byte
```

### 2. Install the required libraries

```bash
pip install -r requirements.txt
```

### 3. Run the notebook

Open:

```text
notebook/House_price.ipynb
```

The notebook downloads the dataset automatically and performs the complete workflow:

**Dataset Download → Data Inspection → Cleaning → Feature Selection → Preprocessing → Train/Test Split → Linear Regression → Evaluation → Predictions → Model Saving → Visualization**

---

## Project Deliverables

This repository contains:

* Jupyter Notebook
* Trained Linear Regression model
* RMSE and R² evaluation results
* Residual plot
* Actual vs predicted plot
* Sample predictions
* Requirements file
* Project documentation

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Joblib
* Requests
* Jupyter Notebook / Google Colab

---

## Conclusion

A Linear Regression model was successfully trained to predict house **price per square foot** from property characteristics.

The model achieved an **RMSE of 3,867.50** and an **R² of 0.3717** on the test set. These results establish a baseline for the dataset and demonstrate the complete workflow of preparing real-world tabular data, training a regression model, evaluating its performance, and saving the trained model for reuse.
