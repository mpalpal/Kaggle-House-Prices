# Kaggle House Prices - Advanced Regression Techniques

This repository contains my solution for the Kaggle competition:

https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques

---

## Overview

The goal of this competition is to predict the final sale price of residential homes using various features describing the property.

This notebook builds a regression pipeline that includes data preprocessing, feature engineering, and model ensembling.

The final prediction is generated using an ensemble of:

- Lasso Regression
- Ridge Regression
- LightGBM

These models were selected to combine the strengths of regularized linear models and gradient boosting trees.

---

## Approach

### Data Preprocessing

The following preprocessing steps were applied:

- Missing value imputation based on feature semantics.
  Especially, in `LotFrontage`, imputation with speculated by a Random Forest model using `LotArea` and `LotConfig` as explanatory variables.
- Converting rankings in categolical columns into meaningful scales to enable a model to understand the relative order of quality
- Creating eight new variables
  1. `TotalSF`: Total floor area of the eintire house (`GrLivArea` + `TotalBamtSF`)
  2. `TotalPorchSF`: Total area of outdoor recreational spaces
  3. `Has2ndFlr`: Whether the house has a 2nd floor or not
  4. `TotalSF_x_Qual`: Total area multiplied by overall quality
  5. `BsmtSF_x_Qual`: Total basement area multiplied by its quality
  6. `HouseAge`: Substract the year of constraction from the year of sale
  7. `YearSinceRemod`: Substract the year of reconstruction from the year of sale
  8. `ToatalBath`: Total number of bath
- Log transformation of `SalePrice` and some explanatory variables with an absolute value of skewness of over 0.75
- One-hot encoding for categorical variables

### Models

Three models were trained and combined using weighted averaging.

**Lasso Regression**

- Uses L1 regularization
- Performs implicit feature selection
- Works well with high-dimensional one-hot encoded data

**Ridge Regression**

- Uses L2 regularization
- Handles multicollinearity between features
- Provides stable linear predictions

**LightGBM**

- Gradient boosting tree model
- Captures nonlinear relationships and feature interactions
- Complements linear models in the ensemble

#### Ensemble

The final prediction is generated using a weighted average of the three models.

Combining linear models and gradient boosting improves robustness and generalization.

---

## Result

- **Public Leaderboard Score:** 0.12242  
- **Rank:** 497 / 4063  
- **Date:** 2026-03-11

---

## License

This notebook is for educational purposes.  
The dataset belongs to the Kaggle competition and must be downloaded from Kaggle.

## Data

Download the dataset from Kaggle:

https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data
