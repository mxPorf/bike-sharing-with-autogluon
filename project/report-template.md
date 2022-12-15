# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Porfirio Basaldua

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
The predictions were non-negative, as the platform required, therefore it sufficed to add them to the provided template and upload the predictions.

### What was the top ranked model that performed?
It was an ensemle model, composed of neural networks and trees. The best model was created after tuning some hyperparameters, and yielded a Kaggle score of 1.79.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
The datasets were already clean (no missing values, no outliers) and already divided into train and test sets. I changed the types as instucted in order to help AutoGluon recognize the data on the columns. I also derived more features from the datetime column.

### How much better did your model preform after adding additional features and why do you think that is?
It performed worse. First I tried creating only one column, containing the year, with this change, the submission score dropped to 1.31 (from 1.74) so I tried creating more columns containing the year, month and day contained in the datetime column, this resulted in almost the same submission score (1.32). Upon reading the documentation, I realized that AutoGluon performs feature engineering on datetime columns, converting the column into an integer timestamp and also extracting the year, month, day and dayofweek from the datetime. Thus, the proposed manual changes were eliminating features instead of adding them, leading to a performance decrease.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
It did better, going from a 1.74 Kaggle score to a 1.79 Kaggle score

### If you were given more time with this dataset, where do you think you would spend more time?
Trying to come with new feature engineering techniques, trying to build upon what was learned and using this step to increment the Kaggle score

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|num_epochs|learning rate|layers|score|
|--|--|--|--|--|
|initial|30|.01|2|1.74775|
|add_features|30|.01|2|1.32708|
|hpo|50|.0001|3|1.79549|


### Create a line plot showing the top model score for the three (or more) training runs during the project.


![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.


![model_test_score.png](img/model_test_score.png)

## Summary
In this project I used AutoGluon as a library to perform a ML pipeline automatically. The library performed feature engineering, trained and tested different models and evaluated their results, finally giving detailed information about the best-performing Machine Learning model. I learned that this pipeline automates a lot of manual work and can serve as a starting point to create a machine learning model that can be further improve, for example, by performing hyperparameter tuning.

To compare the results of the model proposed by AutoGluon, I manually trained and evaluated some individual models: a Random Forest Regressor, a Neural Network and a Linear Regression. The Random Forest Regressor had the best performance, with a RMSE of around 18k, this is significantly worse than the ensemble model produced by AutoGluon, with an RMSE of around 50 (remember that the model performs better if the error is closer to 0)
This results further showcase AutoGluon's capability to create well-performing models.
