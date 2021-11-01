# Report: Predict Bike Sharing Demand with AutoGluon Solution
Neil Simon

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
My initial predictions did not include any negative values, so there was no need to clean them up. That said, for good practice, I verified that all values were non-negative.
I had to add the predictions to a dataframe based on the `sampleSubmissions.csv` file, filling in the `count` column.

### What was the top ranked model that performed?
WeightedEnsemble_L3

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
`datetime` was a poor feature to use as the useful information re day, hour and month was not being considered separately from each other and from the year (the much larger and influencing value).
I realised that atemp and temp were closely related, and that maybe the difference between the two would actually provide useful information for a model.

### How much better did your model preform after adding additional features and why do you think that is?
It performed much better. The predictions went from having a very high error in training (142) and poor result in evaluation by Kaggle (1.33) to giving relatively acceptable results in training (42.1) and evaluation by Kaggle (0.469). I believe that this was predominantly due to the inclusion of `hour` in the feature set.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
My model performed better in training (37.4) but significantly worse in evaluation by Kaggle (0.543) after tuning the hyperparameters. I tried multiple different tunings and none matched the default settings for AutoGluon's Tabular Predictor.

### If you were given more time with this dataset, where do you think you would spend more time?
I would create new features, such as including using the features from previous days to create new features for the current day. Additionally, I would use a lot longer for the training time to further refine the results. I do not believe that hyperparameter tuning is likely to give as significant an increase in performance, but I would continue to examine possible improvements there too.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|num_boost_round|learning_rate|num_trials|score|
|--|--|--|--|--|
|initial|100|1|1024|1.33086|
|add_features|100|1|1024|0.46939|
|hpo|500|0.075|2048|0.54386|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](model_test_score.png)

## Summary
It is clear that AutoGluon's Tabular Predictor is a very capable AutoML tool. It massively simplifies the process of testing different ML models, gives good results without much setup, and has sensibly chosed default settings. This project demonstrated this as after multiple attempts to find better hyperparameters, I was unable to improve on the base results. The only large improvement made was by adding new features to the dataset. By breaking up the `datatime` feature into its components of `hour`, `day`, `month` and `year`, the resulting predictions were much better than before. I suspect that continued creation of new features is the most likely approach to result in better predictions.
