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
			- This means we may have an overall pipeline simply called "data preprocessing," which then opens up into other pipelines. We end up with a great architecture, but at the cost of more debugging complexity.
	- Colab Notebook (Pipelines)
**2) Regularization**: Ways of controlling *overfitting* in the context of reducing the value of regression coefficients. Doing so completely leaves us with the *intercept*, but gives us various methods:
*L2 (Ridge)* and *L1 (Lasso)* or *Elastic Net*, which is `rho L1 + (1-rho) L2`.
**3) Tuning the Model**: #Hyperparameter Optimization. 
	- 

