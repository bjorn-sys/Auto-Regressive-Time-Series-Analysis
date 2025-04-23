# Auto-Regressive-Time-Series-Analysis
AN AUTOREGRESSIVE TIME SERIES ANALYSIS is a kind of time series analysis prediction made assuming the enviroment is stable
it relies on values that are relatively stable overtime to get an accurate prediction
The Readings we predicted was the Air-Quality by using time stamp and the already recorded PM2.5 readings in the data
the dataset used had some columns....
imported all the libraries needed for the analysis...

sensor_id.....the sensor identity number

sensor_type.......the type of sensor that was used in the measurements

location.........location where the measurement was collected

lat..............latitude

lon...............longitude

timestamp...........time and date the measurement was collected

value_type...........the kind of measurement [P1, HUMIDITY, P2, TEMPERATURE, PRESSURE. HDOP]

value..............the values of the measurement 


in this analysis...only time-stamp and the PM2.5 readings was used...
I had to filter out the data that wasn't being used...the timestamp was converted to a datetime format because it came as an object,
and the timezone had to be converted to the designated city [NAIROBI] in africa timezone...after that i needed to resample the data into 1HOUR INTERVALS and used forward fill to fill out the nan values
i could not fill the nan values with mean oe median bcause in time series analysis we can't fill with that...its like judging the present using the past and the future that we haven't lived.
converted the data into series...

ACF--------AUTO-CORRELATION FUNCTION plot was used to check how far in the past we can predict the future with...this shows the correlation coefficient of lag-hours
PACT------PARTIAL AUTO-CORRELATION FUNCTION plot was used to know how many time lags has to be used in prediction
the ACF plot shows a good correlation from 0-2hours, the dipped and rose again around 11, 12, 22-25 hours
the PACF plot shows that the lag hours shouldn't exceede the 26 hour mark so that's the lag hours that was used for prediction
SPLITTING THE DATA----the target column was used as our data set and was splitted between the (y_train)training set[70%] and the (y_test)testing set[30]
the y_train mean was checked.......10.82
the mean_absolute_error baseline......6.32


THE AUTOREGRESSIVE MODEL was used in building the model....fitted the y_train and number of lags=26 and then dropped the nan values that was left by the lags
the mean_absolute_error for the training set.....4.36
residuals which is the observed values - the predicted values plot showed some errors in the data 
the mean_absolute_error for the test set was 5.17 which shouldn't be....the result should be a bit closer to 0


so i corrected it with WALK-FORWARD-VALIDATION
Walk-forward validation is a technique used to evaluate the performance of a model on time series data....
It simulates the real-world scenario where a model is trained on historical data and then used to make predictions on future data.....
Split data: Divide the data into training and testing sets, with the training set being the earlier part of the data and the testing set being the later part.....
Train model: Train the model on the training set.....
Make predictions: Use the trained model to make predictions on the testing set.....
Evaluate performance: Calculate the error between the predicted values and the actual values in the testing set.....
Roll forward: Move the training and testing sets forward in time, retrain the model, and repeat the process.....

After the walk-forward-validation was done the test_mean_absolute_error decreased from 5.17 to 3.44
