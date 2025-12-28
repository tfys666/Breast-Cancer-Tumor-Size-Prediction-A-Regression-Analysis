# Breast-Cancer-Tumor-Size-Prediction-A-Regression-Analysis
## 📋 Overview
This project aims to predict breast cancer tumor size using clinical variables and gene expression data. The analysis combines WGCNA (Weighted Gene Coexpression Network Analysis) for feature selection with LASSO regression and OLS (Ordinary Least Squares) for model building and interpretation. The goal is to identify significant predictors of tumor size and provide insights into their biological relevance.

## 📂 Dataset
The dataset used in this project includes:
- Clinical Variables: Age, lymph node status, ER/HER2 status, histologic grade, menopausal state, cohort, cellularity, and PAM50 subtype.
- Gene Expression Data: Hub genes derived from WGCNA modules (e.g., Brown and Red modules).

## Key Preprocessing Steps:
Missing Value Imputation:
- cellularity: Filled missing values with the mode ("High").
- neoplasm_histologic_grade: Created a "Missing" category and added an indicator variable.

Variable Transformation:
- Log-transformed skewed variables (lymph_node_positive → log(lymph + 1)).
- Standardized continuous variables (e.g., age_scaled).

Dummy Encoding:
- Converted categorical variables (e.g., grade, pam50_subtype) into dummy variables.

## 🔧 Methodology
### 1. Feature Selection
- WGCNA:
  - Identified coexpressed gene modules (e.g., Brown, Red).
  - Selected hub genes (e.g., msh6, acvr1b) based on module membership (kME).
- LASSO Regression:
  - Used 10-fold cross-validation to select the optimal regularization parameter (λ).
  - Reduced 60 candidate features to 23 significant predictors (4 clinical + 19 genes).

### 2. Model Building
- Initial OLS:
  - Fitted an OLS model with LASSO-selected features.
  - Diagnosed model assumptions (residual normality, homoscedasticity, multicollinearity).
- Final OLS:
  - Removed 87 influential points identified via Cook's Distance.
  - Refitted the model on the cleaned dataset.

### 3. Model Evaluation
- Training Set:
  - Improved R² from 0.161 → 0.223 after removing influential points.
  - Adjusted R² = 0.207.
- Test Set:
  - RMSE = 0.45, R² = 0.07.
  - Predictions were stable for typical cases but less accurate for extreme values.

## 📈 Visualizations
- Cook’s Distance Plot: Identified 88 influential points for removal.
- Residual vs Fitted Plot: Confirmed homoscedasticity.
- Prediction vs True Values: Highlighted model performance on the test set.

## 🙏 Acknowledgments
Special thanks to:
- The METABRIC consortium for providing the dataset.
- My collaborators and mentors for their guidance.

Feel free to customize this README further if you have additional details or specific sections you'd like to include!
