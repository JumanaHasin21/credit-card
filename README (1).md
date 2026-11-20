# Credit Card Default Prediction

A machine learning project that explores customer credit-card data and compares classification models to predict whether a customer will default on their next payment.

## Project Overview

The goal of this project is to build and evaluate machine learning classifiers for the target variable **`default payment next month`**.

The notebook follows a data analysis and machine learning workflow:

1. Load the credit-card dataset.
2. Inspect and clean the data.
3. Convert columns to numeric data types.
4. Explore missing values, duplicates, descriptive statistics, and outliers.
5. Treat outliers in selected numerical features using the Interquartile Range (IQR) method.
6. Separate the input features and target variable.
7. Split the data into training and testing sets.
8. Preprocess numerical and categorical features.
9. Select the 20 best features using `SelectKBest` with the ANOVA F-test.
10. Train and evaluate three classification models.
11. Compare model performance using evaluation metrics, confusion matrices, and ROC curves.

## Models Used

The project compares the following classifiers:

- **Logistic Regression**
- **Decision Tree**
- **Random Forest** (100 trees)

## Dataset

The notebook expects the dataset file to be named **`creditcard.xls`**.

Place `creditcard.xls` in the same directory as the notebook before running it.

The prediction target is:

- `default payment next month`

The `ID` column is excluded from model training. The categorical features identified for preprocessing are `SEX`, `EDUCATION`, and `MARRIAGE`.

> The dataset itself is not included in this repository. Make sure you have the right to use and share the dataset before distributing it.

## Data Preprocessing

The notebook performs the following preprocessing steps:

- Removes extra or unnamed index columns where present.
- Converts columns to numeric values.
- Applies IQR-based clipping to selected continuous numerical columns:
  - `LIMIT_BAL`, `AGE`
  - `BILL_AMT1` to `BILL_AMT6`
  - `PAY_AMT1` to `PAY_AMT6`
- Uses a **stratified 80/20 train-test split** with `random_state=42`.
- Imputes numerical missing values using the median.
- Scales numerical features using `StandardScaler`.
- Imputes categorical missing values using the most frequent value.
- Applies one-hot encoding to categorical features.
- Selects the 20 best features using `SelectKBest(score_func=f_classif, k=20)`.

Preprocessing and feature selection are fitted on the training data and then applied to the test data.

## Model Evaluation

The models are evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion matrix
- ROC-AUC
- ROC curve

### Results

The following results were obtained in the notebook:

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8063 | 0.6805 | 0.2344 | 0.3487 | 0.7147 |
| Decision Tree | 0.7127 | 0.3621 | 0.3926 | 0.3767 | 0.6050 |
| Random Forest | **0.8110** | 0.6214 | 0.3723 | **0.4656** | **0.7436** |

### Result Interpretation

Random Forest achieved the highest accuracy, F1-score, and ROC-AUC among the three models, so it was selected as the best overall model in this comparison.

Decision Tree achieved the highest recall, while Logistic Regression achieved the highest precision.

Recall is relatively low for all three models. This means that a considerable number of customers who actually defaulted were classified as non-defaulters. The results should therefore be treated as a baseline rather than a deployment-ready credit-risk system.

## Technologies and Libraries

- Python
- Jupyter Notebook
- NumPy
- pandas
- Matplotlib
- Seaborn
- scikit-learn
- xlrd (for reading the `.xls` dataset)

## Installation

Install the required libraries:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn xlrd openpyxl jupyter
```

## How to Run

1. Clone or download this repository.
2. Place `creditcard.xls` in the same folder as `CreditCard.ipynb`.
3. Install the dependencies listed above.
4. Start Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

5. Open `CreditCard.ipynb`.
6. Run the notebook cells in order, from top to bottom.

## Project Structure

```text
Credit-Card-Default-Prediction/
│
├── CreditCard.ipynb
├── creditcard.xls        # Dataset file; not included
└── README.md
```

## Limitations and Future Improvements

- Improve recall so that more actual defaulters are identified.
- Explore class-imbalance handling techniques, where appropriate.
- Tune model hyperparameters using cross-validation.
- Evaluate threshold adjustments based on the cost of false negatives and false positives.
- Validate the final model on additional data before considering real-world use.

## Conclusion

This project demonstrates an end-to-end baseline classification workflow for credit-card default prediction. Among the tested models, Random Forest delivered the strongest overall balance according to F1-score and the highest ROC-AUC. However, its recall indicates that further work is needed before the model could be considered suitable for practical credit-risk decisions.
