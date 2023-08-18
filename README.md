Goal- 
The dataset contains information about customer bookings of an airline. Train a classification model which will predict whether or not a customer will make a booking. This model will help the airline companies to understand their customer's behaviour, which will result in increased number of bookings for them.

Solution Approach- 
First data cleaning is done, followed by data visualization using seaborn.

Some categorical columns have a large number of classes, so creating dummy variables for each class will result in hundereds of new features. 
To avoid this, I have taken the top 25 classes with most number of records in categorical column, then created dummy variables for only these 25 classes. Same is repeated for all categorical columns with large number of classes.

The dataset provided is imbalanced so use undersampling to make the number of observations of majority class equal to number of observations in minority class. 
Then I have used Hyperparameter tuning to get the best possible values for the parameters used in XGBoost.

Created 2 models- XGBoost with default parameters and XGBoost with hyperparameter tuned paramters.

Result- XGBoost with hypertuned parameters is giving a higher acccuracy and f1 score.
Accuracy of the model- 71.28% 
F1 Score of the model- 72.02%

A detailed explaination of all the steps-
The dataset contains 50002 entries.
The features in the dataset-
1. num_passengers
2. sales_channel
3. trip_type
4. purchase_lead
5. length_of_stay
6. flight_hour
7. flight_day
8. route
9. booking_origin
10. wants_extra_baggage
11. wants_preferred_seat
12. wants_in_flight_meals
13. flight_duration
14. booking_complete (Dependent variable)

A high level walk through of the steps I followed to make the model-
1. Import all the required libraries and dataset.
2. Remove all dublicate rows from the dataset.
3. Check if dataset has rows with null values. It does have such rows.
4. Check dataset details using describle method. There are outliers in length_of_stay column (compare the 75% and max, there's a huge difference.)
#We can remove outliers in length_of_stay column since it is unlikely that length of stay is 778 hours for anyone.
5. Remove outliers from length_of_stay column.
6. Used seaborn to do data visualization of the dataset.
7. Scale all numerical values.
8. Check the number of classes present in categorical columns.
   sales_channel     2
   trip_type     3
   flight_day     7
   route     796
   booking_origin     103
9. Number of classes is less in sales_channel, trip_type and fligt_day so created dummies variables for these categorical columns.
10. route and booking_origin has a lot of classes so replacing them with dummy columns will result in (796+103=900) new columns! That is too many new features, so instead, I picked the top 25 classes with most number of entries in each of the two columns and created dummy columns for these 25 classes.
11. Drop route and booking_origin column since they are replaced by their dummy columns.
12. Divide into test and train dataset.
13. Use hyperparameters tuning on XG Boost to get the best possible result.
14. Try with default XG Boost parameters as well.
15. Accuracy of hyper parmeter tuned XG Boost- 0.8526462191640436
    F1 Score of hyper parmeter tuned XG Boost- 0.10413885180240322
16. Accuracy is fine but f1 Score is very low (around only 10%).
17. F1 score is low because it is an imbalanced dataset. Number of 0s in booking_complete is much more than 1s. 
18. Do undersampling, i.e., reduce the number of rows that are classified 0 to be equal around the number of rows that are classified as 1.
19. Make the hyperparameters tuned on XG Boost model and default XG Boost model again.
20. This time the accuracy of hyperparameter tuned XG Boost model is around 71% and F1 score is around 72%.
    This is much better f1 score than what we were getting before undersampling. 
