# ✈️ Flight Price Prediction Using Machine Learning

## 📌 Project Overview

**Flight Price Prediction** is a Machine Learning project that predicts airline ticket prices based on different flight-related features such as airline, source, destination, number of stops, journey date, departure time, arrival time, and flight duration.

The project follows a complete Machine Learning workflow, including **data cleaning, feature engineering, exploratory data analysis, outlier handling, feature selection, model training, and evaluation**.

A **Random Forest Regressor** is used to learn the relationship between flight characteristics and ticket prices and predict the expected price of a flight.

---

## 🎯 Project Objective

The main objectives of this project are:

* Analyze historical flight price data.
* Clean and preprocess the dataset.
* Handle missing values and outliers.
* Extract useful features from date and time information.
* Convert categorical variables into numerical features.
* Analyze relationships between flight characteristics and ticket prices.
* Identify important features using Mutual Information.
* Train a Machine Learning regression model.
* Predict flight ticket prices.
* Evaluate model performance using the R² score.

---

## 🛠️ Technologies and Libraries Used

* **Python** – Programming language
* **Pandas** – Data manipulation and preprocessing
* **NumPy** – Numerical operations
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical visualization
* **Scikit-learn** – Machine Learning
* **Random Forest Regressor** – Price prediction model

---

## 📂 Dataset

The project uses a flight dataset stored in an Excel file:

```text
Data_Train.xlsx
```

The dataset contains information about flight journeys and their corresponding ticket prices.

Important columns include:

* `Airline`
* `Date_of_Journey`
* `Source`
* `Destination`
* `Route`
* `Dep_Time`
* `Arrival_Time`
* `Duration`
* `Total_Stops`
* `Additional_Info`
* `Price`

The target variable is:

```text
Price
```

---

## 🔄 Project Workflow

```text
Load Dataset
      ↓
Data Cleaning
      ↓
Handle Missing Values
      ↓
Date & Time Feature Engineering
      ↓
Flight Duration Processing
      ↓
Exploratory Data Analysis
      ↓
Categorical Feature Encoding
      ↓
Outlier Handling
      ↓
Feature Importance Analysis
      ↓
Train-Test Split
      ↓
Random Forest Regressor
      ↓
Price Prediction
      ↓
Model Evaluation
```

---

## 🧹 Data Cleaning

The following preprocessing steps were performed:

1. Loaded the dataset using Pandas.
2. Checked dataset information and data types.
3. Checked for missing values.
4. Removed rows containing missing values.
5. Converted date and time columns into proper datetime format.
6. Extracted useful features from dates and times.
7. Processed flight duration.
8. Converted categorical features into numerical representations.
9. Removed unnecessary columns.
10. Identified and handled extreme price values.

---

## 📅 Date Feature Engineering

The `Date_of_Journey` column was converted into datetime format.

New features were extracted:

* `Journey_day`
* `Journey_month`
* `Journey_year`

These features help the model understand how ticket prices may vary depending on the date of travel.

The original `Date_of_Journey` column was removed after extracting the required information.

---

## ⏰ Time Feature Engineering

The `Dep_Time` and `Arrival_Time` columns were converted into datetime format.

The following features were extracted:

### Departure Time

* `Dep_Time_hour`
* `Dep_Time_minute`

### Arrival Time

* `Arrival_Time_hour`
* `Arrival_Time_minute`

This allows the model to understand the relationship between departure/arrival times and ticket prices.

---

## 🌅 Flight Departure Time Categories

Departure hours were also categorized into different time periods:

* Late Night
* Early Morning
* Morning
* Noon
* Evening
* Night

This analysis helps identify the distribution of flights across different times of the day.

---

## ⏱️ Flight Duration Processing

The `Duration` column contains values such as:

```text
2h 50m
5h 30m
1h 20m
```

The duration was processed to extract:

* `Duration_hours`
* `Duration_mins`
* `Duration_total_mins`

This converts flight duration into numerical information that can be used by the Machine Learning model.

---

## 📊 Exploratory Data Analysis

Several visualizations were created to understand the relationship between flight characteristics and ticket prices.

### Duration vs Price

A scatter plot was used to analyze whether longer flight durations are associated with higher ticket prices.

### Duration vs Price by Stops

The relationship between flight duration, price, and number of stops was analyzed.

### Airline vs Price

A box plot was created to compare ticket price distributions across different airlines.

This analysis helps identify airlines with relatively higher or lower average ticket prices.

---

## 🏷️ Categorical Feature Encoding

Machine Learning models require numerical input, so categorical features were converted into numerical representations.

### Source Encoding

One-hot encoding was applied to the `Source` column.

For example:

```text
Source_Delhi
Source_Kolkata
Source_Mumbai
Source_Chennai
```

The value is:

```text
1 → Category matches
0 → Category does not match
```

---

### Airline Encoding

Airlines were ranked based on their average ticket prices.

The average price of each airline was calculated, and the airlines were assigned numerical values based on their sorted average prices.

---

### Destination Encoding

The `Destination` column was also converted into numerical values based on the average ticket price associated with each destination.

`New Delhi` was combined with `Delhi` to avoid treating them as separate destinations.

---

### Total Stops Encoding

The number of stops was converted into numerical values:

| Flight Type | Value |
| ----------- | ----: |
| Non-stop    |     0 |
| 1 stop      |     1 |
| 2 stops     |     2 |
| 3 stops     |     3 |
| 4 stops     |     4 |

This allows the model to understand the relationship between the number of stops and ticket prices.

---

## 🗑️ Feature Removal

The following columns were removed because they were either redundant, unnecessary, or no longer required after feature extraction:

* `Date_of_Journey`
* `Additional_Info`
* `Duration_total_mins`
* `Source`
* `Journey_year`
* `Route`
* `Duration`

The final dataset contains the processed numerical features used for Machine Learning.

---

## 📈 Outlier Detection and Handling

The distribution of ticket prices was analyzed using:

* Distribution plots
* Box plots

The Interquartile Range (IQR) method was used to understand potential outliers.

The project also replaces extremely high prices, specifically prices greater than or equal to **35,000**, with the median ticket price.

This step was performed to reduce the effect of extreme values on the regression model.

> **Note:** In a production project, it would be better to justify this threshold using domain knowledge or use a statistically derived outlier treatment method rather than using a fixed value without validation.

---

## 🔍 Feature Importance Using Mutual Information

**Mutual Information Regression** was used to analyze the relationship between input features and the target variable.

```python
from sklearn.feature_selection import mutual_info_regression

imp = mutual_info_regression(X, y)
```

The resulting importance scores help identify which features contain the most useful information for predicting flight prices.

---

## 🤖 Machine Learning Model

The project uses:

### Random Forest Regressor

Random Forest is an ensemble Machine Learning algorithm that combines multiple decision trees to produce a more robust prediction.

It is suitable for this project because it can:

* Capture non-linear relationships.
* Handle complex interactions between features.
* Work with multiple numerical features.
* Provide strong performance for many regression problems.

The model is trained using:

```python
from sklearn.ensemble import RandomForestRegressor

ml_model = RandomForestRegressor()
ml_model.fit(X_train, y_train)
```

---

## ✂️ Train-Test Split

The dataset was divided into:

* **75% Training Data**
* **25% Testing Data**

The training dataset is used to train the Random Forest model.

The testing dataset is used to evaluate how well the model predicts prices for unseen data.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.25,
    random_state=42
)
```

---

## 🔮 Price Prediction

After training the model, predictions are generated using:

```python
y_pred = ml_model.predict(X_test)
```

The predicted prices are compared with the actual prices from the testing dataset.

---

## 📊 Model Evaluation

The model is evaluated using the **R² Score**.

```python
metrics.r2_score(y_test, y_pred)
```

### R² Score

R², or the coefficient of determination, measures how well the model explains the variation in flight prices.

A higher R² score generally indicates better predictive performance.

Other useful metrics that can be added include:

* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)
* Root Mean Squared Error (RMSE)
* Mean Absolute Percentage Error (MAPE)

---

## 💡 Key Features of the Project

* ✈️ Flight ticket price prediction
* 🧹 Data cleaning and preprocessing
* 📅 Date feature extraction
* ⏰ Time feature extraction
* ⏱️ Flight duration processing
* 🛫 Airline analysis
* 🌍 Source and destination analysis
* 🛑 Number of stops analysis
* 📊 Exploratory Data Analysis
* 📦 Outlier detection and treatment
* 🔍 Mutual Information feature analysis
* 🌲 Random Forest Regression
* 📈 R²-based model evaluation

---

## 🚀 Future Improvements

The project can be improved by:

* Using `OneHotEncoder` with a Scikit-learn Pipeline for categorical variables.
* Applying proper train-test separation before target-based encoding to prevent data leakage.
* Using cross-validation.
* Performing hyperparameter tuning using `GridSearchCV` or `RandomizedSearchCV`.
* Comparing Random Forest with XGBoost, Gradient Boosting, and LightGBM.
* Adding MAE, RMSE, and MAPE evaluation metrics.
* Creating a web application using Streamlit or Flask.
* Deploying the trained model as an API.
* Adding real-time flight data and dynamic pricing information.
* Using a statistically validated method for handling price outliers.

---

## 🎓 Learning Outcomes

Through this project, I gained practical experience in:

* Python programming
* Data preprocessing
* Exploratory Data Analysis
* Feature engineering
* Date and time manipulation
* Categorical encoding
* Outlier detection
* Feature selection
* Mutual Information
* Regression Machine Learning
* Random Forest
* Model evaluation

---

## 📌 Project Summary

This project demonstrates how Machine Learning can be used to predict flight ticket prices based on historical flight information. The dataset is cleaned and transformed through feature engineering, categorical encoding, and outlier handling. Important features are analyzed using Mutual Information, and a **Random Forest Regressor** is trained to predict flight prices.

The project covers an end-to-end Machine Learning workflow, from **data preprocessing and exploratory analysis to model training, prediction, and evaluation**.

---

## 📝 Resume Description

> Developed a Flight Price Prediction system using Python and Machine Learning. Performed data preprocessing, date-time feature engineering, categorical encoding, exploratory data analysis, outlier handling, and feature selection using Mutual Information. Trained a Random Forest Regressor to predict flight ticket prices and evaluated model performance using the R² score.

---

## ⭐ Short Project Description

> **Flight Price Prediction** is a Machine Learning project that predicts airline ticket prices using features such as airline, destination, source, departure time, arrival time, flight duration, and number of stops. The project uses feature engineering, exploratory data analysis, Mutual Information, and a Random Forest Regressor to build and evaluate the price prediction model.
