
🔁 Auto-Regressive Model Time Series Analysis

📘 Overview

This project explores the use of an Auto-Regressive (AR) model for time series forecasting. The goal was to predict air quality (PM2.5 levels) using historical time-stamped data under the assumption of a relatively stable environment. The model leverages past observations to predict future values, relying on autocorrelation within the dataset.


---

🧾 Dataset Description

The dataset consists of environmental sensor data with the following columns:

> Focus: For this analysis, only PM2.5 (P2) readings were used along with timestamps.




---

⚙️ Data Preprocessing

Filtered the dataset to include only P2 values (PM2.5)

Converted the timestamp column from object to datetime format

Localized time to the Africa/Nairobi timezone

Resampled the data to hourly intervals

Used forward-fill (ffill) to fill in missing values — forward fill respects time order and is preferable over mean/median in time series



---

🛠️ Feature Engineering

Converted the filtered dataset into a series

Applied ACF (Auto-Correlation Function) to assess how far into the past we can predict the future

Applied PACF (Partial Auto-Correlation Function) to determine optimal lag length


🔍 ACF & PACF Observations

ACF showed strong correlations up to 2 hours, with notable patterns around lags 11–12 and 22–25

PACF indicated that the effective number of lags should not exceed 26 hours



---

🔄 Model Training: Auto-Regressive Model (AR)

Training/Test Split:

y_train: 70% of the data

y_test: 30% of the data


Baseline Mean of y_train: 10.82

Baseline Mean Absolute Error (MAE): 6.32

AR Model Configuration:

Used 26 lag values

Trained only on y_train

Dropped NaN values introduced by lagging


Model Evaluation:

Training MAE: 4.36

Testing MAE: 5.17 — slightly high, indicating overfitting or insufficient generalization




---

🔁 Walk-Forward Validation

To improve model robustness and simulate a real-world deployment scenario, walk-forward validation was implemented.

✅ Steps in Walk-Forward Validation

1. Split: Begin with a standard train/test split


2. Train: Fit the model on the training data


3. Predict: Make a prediction for the next time step


4. Evaluate: Calculate prediction error


5. Roll Forward: Add the actual observed value to the training set, repeat the steps above



🔽 Result After Walk-Forward Validation

Improved Test MAE: 3.44
This shows a significant improvement over the initial AR model's test error (5.17).



---

📌 Key Insights

AR models can effectively model stable time series environments with strong autocorrelation

Optimal lag selection using ACF/PACF is critical to model performance

Walk-forward validation provides a realistic and more accurate assessment of time series model performance

Prediction accuracy improves as the model continually adapts to recent trends



---
