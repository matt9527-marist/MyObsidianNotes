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
		- `make.column.transformer`
**2) Regularization**: Ways of controlling *overfitting* in the context of reducing the value of regression coefficients. Doing so completely leaves us with the *intercept*, but gives us various methods:
*L2 (Ridge)* and *L1 (Lasso)* or *Elastic Net*, which is `rho L1 + (1-rho) L2`.
**3) Tuning the Model**: #Hyperparameter Optimization. 


