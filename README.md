# Video_Engagement_score
## Approach for solving the code

### Objective:

The main objective of the problem is to develop the machine learning approach to predict the engagement score of the video on the user level.

### Approach:

The dataset contains 89197 data points and 10 columns of features.
* Columns : ['row_id','user_id','category_id','video_id', 'age', 'gender','profession',     'followers', 'views', 'engagement_score']
* All the columns are of int & float type except gender & profession belonging to the object type.
* There are no missing values in the dataset.
* Dropped the row_id.

On finding Correlation using heatmaps there is not much correlation observed between any features. But, a notable correlation is observed between category_id & video_id(0.56)
* But removing any one feature in the correlated features(category_id & video_id) is not having a positive effect on the R2-score metric. Hence using both as it is.

Text preprocessing
* One-hot encoding of the categorical feature is done.
* Label encoding doesn't have a positive effect on the R2-score metric. Hence one-hot encoding is preferred because the categorical features are nominal in nature.
* Standardization of numerical features had no effect on the performance metric. Hence no scaling is done on the data.
* The number of followers and views have an effect on the engagement score.
  + Tried applying some basic mathematical operations(logarithmic, Inverse) on the columns, but had no effect on increasing the performance metric.
  + But creating a new feature combining both views & performance led to a slight increase in performance metrics.
  + feat1_v/f = views/followers

Splitting the Main training data into 80% train and 20% test data for model building and evaluation of performance.
* Used two models i.e, Random Forest and XGBRegressor on the data.
* Tried applying linear models such as linear regression and SVM but there is very little R2-score and SVM computation took a lot of time for hyper-parameter tuning.
* RandomForest is applied 
  + Hyper-parameter tuning with n_estimators,min_samples_split is done to find the best parameters.
  + n_estimators = 200,min_samples_split = 3 is finally used to build the model.
* XGBRegressor is applied
  + Hyper-parameter tuning with n_estimators is done to find the best parameter.
  + n_estimators = 300,max_depth = 10 is used to buid the model.
* Finally, the metrics observed from both are 

![github](https://user-images.githubusercontent.com/50799650/156925492-9e23234c-cdf2-4943-8b8f-d5922efe8a22.JPG)

* But on the final test data provided to score the model XGboost gave the highest R2-score.Hence final submission.csv is submitted accordingly.
