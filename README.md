# Multivariate Time Series Regression and Classification

In this task, the goal is to apply ML and DL algorithms on two classification problems and one regression problem. The overview of the dataset is stated below:

1. Individual household electric power consumption : Measurements of electric power consumption in one household with a one-minute sampling rate over a period of almost 4 years. Different electrical quantities and some sub-metering values are available. 

2. EEG Eye State: All data is from one continuous EEG measurement with the Emotiv EEG Neuroheadset. The duration of the measurement was 117 seconds. The eye state was detected via a camera during the EEG measurement and added later manually to the file after analysing the video frames. '1' indicates the eye-closed and '0' the eye-open state. All values are in chronological order with the first measured value at the top of the data.

3. Occupancy Detection: Experimental data used for binary classification (room occupancy) from Temperature,Humidity,Light and CO2. Ground-truth occupancy was obtained from time stamped pictures that were taken every minute.

## Work flow

**1. Background understanding of Time Series**:

**Time Series:** Time series data is a type of data where observations are recorded in chronological order over a period of time. Each data point in a time series is associated with a specific time or date. Time series data can be categorized into two main types, univariate time series and multivariate time series. Datasets used in this task are example of multivariate time series data. 

Multivariate time series involves multiple (more than one) time-dependent variables, and each data point represents the values of these variables at a specific time. Each variable depends not only on its past values but also has some dependency on other variables. This dependency is used for forecasting future values. A model that makes use of multiple input variables may be referred to as a multivariate multi-step time series forecasting model. The goal of analyzing multivariate time series is to study the relationships and dependencies among the variables and make predictions for each variable based on their historical values. Common examples of multivariate time series include macroeconomic indicators (e.g., GDP, inflation, unemployment), where multiple economic variables are observed over time.

**2. Loading the dataset and Preprocessing**: I have loaded the dataset and converted the date column to a datetime format to work with time series data. I have checked for missing value and handled outliers using empirical rule. The Empirical Rule states that 99.7% of data observed following a normal distribution lies within 3 standard deviations of the mean. Under this rule, 68% of the data falls within one standard deviation, 95% percent within two standard deviations, and 99.7% within three standard deviations from the mean. Z-scores represent the number of standard deviations a data point is away from the mean. 

**3. Exploratory Data Analysis (EDA):** I have demonstrated several plots for the purpose of analysis and finding insights. For example, in the occupancy dataset, I have observed occupants in the environment between 07:00 am and 5.00 pm. Then I added one more column using that information. In the power consumption dataset, I have performed resampling in the "global_active_power" column over day, month, quarter year, hour. Resampling by month, day or hour is very important because it has a large impacts (changing the periodicity of the system). But, if processing all the original data, the runtime will be very costly. Again, If I process the data with large time-scale samples (e.g. monthly), it will affect the model's predictivity. That's why it is relatively reasonable to resample data by hour.

**4. Train-Test Split**: In household power consumption problem, I took 1 year data for training and chose 1 hour time step. I split the eye state data into a training set (80%) and a test set (20%). I did not did any split on occupancy dataset as there were already three datasets in the data repository. I chose them as train, validation, and test set.

**5. Model Building, Prediction and Evaluation**:

I have built LSTM and Vector Autoregression model for the power consumption problem. I used RMSE as the evaluation metric.

On the EEG Eye state data, I have applied Extra Trees Classifier, XGBoost, and LSTM for eye state prediction.

I have applied Extra Trees Classifier, XGBoost, and Simple Feedforward Neural Network for detecting occupancy.

For the classification problems I have used Accuracy, ROC sscore, F1 score, confusion matrix for evaluation.

## Result

- In the Individual household electric power consumption, LSTM performed better than VAR in forecasting the global active power.

- In the EEG Eye state problem, Extra Trees Classifier has the highest accuracy and f1 score of 95.23% and 94.77% respectively.

- In the Occupancy detection problem, Extra Trees Classifier and Simple FNN both achieved almost similar kind of result. When applied the models on test data, Extra Tree Classifier has achieved accuracy of 0.978466 and f1 score of 0.951095. With Simple FNN, accuracy and f1 score achieved were 0.978363 and 0.950804 respectively.

## Conclusion

To conclude, I have fulfilled the task objective by appling ML and DL algorithms on two classification problems and one regression problem. By analyzing the outcomes, I have obtained valuable insights into the predictive capabilities of different algorithms for multivariate time series data and their effectiveness in solving energy consumption forecasting and classification problems. The task aims to demonstrate the suitability of different approaches and guide the selection of appropriate algorithms for different types of multivariate time series analysis.
