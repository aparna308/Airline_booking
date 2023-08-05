The dataset contains information about previous customer bookings. Based on past records, I've trained a model which will predict whether or not the customer will make a booking.
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
10. route and booking_origin has a lot of classes so replacing them with dummy columns will result in (796+103=900) new columns! That is too many columns, so instead, I picked the top 25 classes with most number of entries in each of the two columns and created dummy columns for these 25 classes.
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
20. This time the accuracy of hyperparameter tuned on XG Boost is 0.7101484546118277 (71%) and F1 score is 0.7145938173975557 (71%).
21. This is much better result than last time.
