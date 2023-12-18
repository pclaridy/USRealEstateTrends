# Unveiling American Real Estate: A Comprehensive Analysis of Residential Listings

This initiative embarks on a detailed exploration of the dynamic landscape of the U.S. residential real estate market. Leveraging a comprehensive dataset from Zillow, a leading real estate database, this project aims to dissect and interpret the complexities and trends of property listings across various regions of the United States.

## Description

The core of this analysis is the 2023 Zillow House Listings dataset. This extensive collection of data provides an in-depth view of a wide array of homes across the U.S., offering a unique lens through which to analyze and understand the real estate market's various dimensions.

## Data Source

This project utilizes a dataset sourced from [Kaggle](https://www.kaggle.com/datasets/febinphilips/us-house-listings-2023), which encompasses a wealth of information about residential properties across the United States for the year 2023. The original compilation of this data is credited to Zillow, a prominent player in the real estate and rental marketplace. The dataset is rich with property-specific details, including physical attributes, Zillow's Zestimate® of property value, Rent Zestimate®, and the actual listing price. This extensive dataset provides a granular view of the housing market, enabling a comprehensive analysis of real estate trends, valuations, and rental market dynamics across various regions in the U.S.

## Table of Contents

- [Description](#description)
- [Data Source](#data-source)
- [Installation](#installation)
- [Data Preprocessing](#data-preprocessing)
- [Modeling](#modeling)
- [Model Evaluation and Validation](#model-evaluation-and-validation)
- [Hyperparameter Tuning](#hyperparameter-tuning)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgments](#acknowledgments)

## Installation

```bash
git clone https://github.com/pclaridy/USRealEstateTrends.git
cd USRealEstateTrends
```
### Data Preprocessing

For this project, a meticulous data preprocessing approach was adopted to ensure high-quality input for the predictive models. Each step was carefully executed to enhance data integrity and relevance:

- **Initial Inspection and Cleaning**:
  - **Data Loading**: Loaded the dataset from a CSV file for initial exploration.
  - **ZIP Code Transformation**: Converted ZIP codes to strings to maintain the format.
  - **Missing and Zero Value Analysis**: Investigated and quantified the extent of missing and zero values.
  - **Handling Missing 'Price' Values**: Removed rows with missing or zero 'Price' values.

- **Data Imputation and Transformation**:
  - **Categorical Columns**: Imputed missing values in 'State', 'City', and 'Street' with 'Unknown'.
  - **KNN Imputation for 'Area'**: Replaced zeros with NaNs and employed KNN imputation to estimate missing 'Area' values based on neighboring data points.
  - **Handling Outliers**: Applied Interquartile Range (IQR) method to identify and handle outliers in numerical columns.
  - **Frequency Encoding**: Applied to 'City' and 'Street' columns for managing categorical complexity.

- **Advanced Data Imputation**:
  - **Preparation for RandomForestRegressor**: Ensured no NaN values in predictor columns ('Price', 'Bedroom', 'Bathroom', 'Area') before advanced imputation.
  - **RandomForestRegressor for Market and Rent Estimates**: Employed RandomForestRegressor for imputing missing values in 'MarketEstimate' and 'RentEstimate', considering multiple feature relationships.

- **Data Analysis and Finalization**:
  - **Correlation Analysis**: Explored relationships between 'MarketEstimate', 'RentEstimate', 'Price', and other variables.
  - **Correlation Matrix Visualization**: Used heatmap visualization to understand correlations among numerical variables.
  - **Final Missing Value Check**: Ensured all missing values were appropriately addressed.
  - **Exporting Cleaned Data**: Saved the preprocessed dataset as a Pickle file to preserve data structure and types.

Each preprocessing step was integral in transforming the raw dataset into a refined format, ready for effective modeling and analysis.

### Modeling

In this real estate price prediction project, I employed a diverse array of machine learning models to understand and forecast property prices. The selection of models was based on their ability to handle regression tasks effectively. Here's an overview:

- **Linear Models**:
  - **LinearRegression**: A baseline model for its simplicity and interpretability.
  - **Lasso**: Useful for its ability to perform feature selection by shrinking coefficients of less important features to zero.
  - **Ridge**: Tackles multicollinearity (high correlation among features) by imposing a penalty on the size of coefficients.
  - **ElasticNet**: Combines features of both Lasso and Ridge, making it robust against various data peculiarities.

- **Tree-Based Models**:
  - **DecisionTreeRegressor**: Offers a deep level of insight with its hierarchical structure of decision nodes and leaves.
  - **RandomForestRegressor**: An ensemble of decision trees, it improves prediction accuracy and controls over-fitting.
  - **GradientBoostingRegressor**: Boosts weak learners sequentially to improve model performance.
  - **XGBRegressor**: An efficient implementation of gradient boosting, known for its speed and performance.

- **Other Models**:
  - **KNeighborsRegressor**: A non-parametric method that predicts values based on the similarity (or ‘nearness’) to known cases.
  - **SVR (Support Vector Regression)**: Adapts the margins of decision boundary to get more robust predictions.
  - **MLPRegressor (Multi-layer Perceptron Regressor)**: A neural network model capable of capturing complex relationships in data.

Each model was chosen for its unique strengths and ability to provide different perspectives on the dataset. This diverse set allows for a comprehensive exploration of the data, ensuring robust and reliable predictions.

### Model Evaluation and Validation

Model evaluation and validation were integral to ensuring the accuracy and generalizability of the predictions. The following strategies were employed:

- **K-Fold Cross-Validation**: This method splits the dataset into 'k' consecutive folds while ensuring every observation gets to be in a test set exactly once. It provides a robust way to assess model performance. In this project, a 5-fold cross-validation was used, balancing computational efficiency with robustness.

- **RMSE (Root Mean Squared Error)**: Used as a primary metric to evaluate model performance. It measures the average magnitude of the errors between predicted and actual values, giving more weight to large errors.

- **R² Score**: Employed as a supplementary metric, it represents the proportion of variance in the dependent variable that's predictable from the independent variables. It gives an idea of the goodness of fit of a model.

### Hyperparameter Tuning

Hyperparameter tuning was conducted to optimize each model's performance. This process involved:

- **RandomizedSearchCV**: This method was used for its efficiency in searching through a large hyperparameter space. It randomly selects a subset of the parameter combinations, allowing for a broad yet computationally feasible search.

- **Parameter Grids**: Specific for each model, they included parameters like `n_estimators`, `max_depth`, and `learning_rate` for tree-based models, `C` and `kernel` for SVR, and `hidden_layer_sizes` and `activation` for MLPRegressor. The choice of parameters was based on their potential impact on model performance.

- **Impact on Performance**: Hyperparameter tuning allowed for the refinement of each model, often resulting in improved RMSE scores. It helped in identifying the best-performing model configurations, which were crucial in making accurate predictions.

This meticulous approach to modeling, evaluation, and hyperparameter tuning ensured the robustness and reliability of the predictive models, thus enabling accurate real estate price predictions.

