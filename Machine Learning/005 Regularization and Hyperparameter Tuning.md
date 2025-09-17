## Overview
**1) Data Preprocessing**: | SkLearn and Pandas: 
	- Deal with missing data 
	- Alphanumeric data --> Encoding (One-Hot Encoding, Dummy Variables, etc.)
	- Numeric data: may need to scale the data. 
		- *Standard Scaler*: Use Z-scores 
		- *Min/Max*
	- SkLearn manages *Estimators*: (shortcut is fit-transform)
		- *Transformers*: fit/transform or `fit.transform()`
		- *Predictors*: fit/predict, use the trained data to predict new data.
	Also in terms of SKLearn:
		- Column Transformer: `CT = make_column_transformer(tuple_1, tuple_2...)`
		- tuple: ( [estimator], [list features])
			- We can use a pipeline for the estimator input. SKLearn has a useful operation make_pipeline, instantiating a pipeline object that will possess a select number of steps. 
			- `pl = make_pipeline(SimpleImputer(), StandardScaler()`
			- This means we may have an overall pipeline simply called "data preprocessing," which then opens up into other pipelines for further transforming the data. We end up with a great architecture, but at the cost of more debugging complexity.
	- [Colab Notebook (Pipelines)](https://gist.github.com/eitellauria/b3ad40e871ba13643de353f20cf4a582)
**2) Regularization**: Ways of controlling *overfitting* in the context of reducing the value of regression coefficients. Doing so completely leaves us with the *intercept*, but gives us various methods:
*L2 (Ridge)* and *L1 (Lasso)* or *Elastic Net*, which is `rho L1 + (1-rho) L2`.
**3) Tuning the Model**: #Hyperparameter Optimization. 
	- *Cross Validation*: suppose we have a dataset split into training and testing data. We will divide the training dataset TR into K folds (fractions) of the same size. 
		- Suppose we need to tune our model. We will train the model with all of the TR data, but we will leave the first fold `k=1` out of the training. Compute RMSE or MAE (1)
		- In the next training iteration, we will leave out the second fold `k=2`. Compute RMSE or MAE (2)
		- Repeat this process `k` times. 
		- We end up with RMSE and MAE (k). 
	- Why do we do this? Let's assume we are using *Elastic Net*, where we are using lambda (learning rate) and rho (how much of ridge vs. how much of lasso we are using). These are two **hyperparameters**. These are the values we want to tune. We shouldn't be testing these hyperparameters against the final testing data. Instead, we are using *validation data* to test them.

