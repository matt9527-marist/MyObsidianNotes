**1) Missing Data**
Consider a dataset that has NULL values or missing cells. We have some options:
- Eliminate the row containing the missing data:
	- Can work for few occurrences of missing data
	- Can bias the data by obscuring the reason why there is missing data
- Place a threshold on certain columns/features that decide whether or not to eliminate the feature altogether if the percentage of missing data passes that threshold. 
- *Imputation* - take those columns where we having a NULL value and replace it with some value. How we do this depends on the data. This can be done using the other values in the dataset as the training set to train a model, and then use the model to predict the target missing value.
	- Numerical data: use average or median value. 
	- Discrete / alphanumeric data: use the mode.

**2) Data Encoding** (Particularly with alphanumeric data)
The algorithms we work with have no use with strings of data. 
Recall:$$\hat{y} = w_{0} + w_{1}x_{1} + w_{2}x_{2} + w_{3}x_{3} \dots$$
The coefficients are saying that a unitary increase in the value of say, x1, will introduce a change in y_hat which is equivalent to this value w1 if all of the other features remain constant. This is for scaled values. The distance between 1 and 2, or 2 and 3 is completely meaningless for alphanumeric values (Japan vs. New York for a location feature).
In Pandas, we can use dummy variables to solve this problem. In Scikit Learn, this is referred to as **One-Hot Encoding**.

Imagine we have the column:

*Origin*                            [        Dummy Values        ]
![[Pasted image 20250915161852.png]]

**3) Scaling**

> Why do we scale the values? What if the features we use are very different from each other? If one feature has values far higher than another feature, it can overpower it. 

How do we normalize the data?
- Min/Max Scaling:
$$X_{Scaled} = \frac{X - X_{Min}}{X_{Max} - X_{Min}}$$
- Standard Scaling:
	- *Z-scores: $$Z = \frac{X - \bar{X}}{\sigma_{x}}$$
	- Note: if we standardize things in this way, this means we are then measuring our data in terms of standard deviations. 
The Min/Max scaling option is far more commonly used than Z-scores. Z-scores simply allow us to use more varied ranges of values, such as negative values, more than just the range of 0-1.

[Data Pre-processing in Scikit Learn](https://gist.github.com/eitellauria/8f7e053bbe00cd1aaf6f5db6748e97b5)

The following figure illustrates how a **transformer**, fitted on the training data, is used to transform a training dataset as well as a new test dataset:
![[Pasted image 20250915163959.png]]

We can use #LinearRegression in an estimator to be a **predictor** for the dataset. 

![[Pasted image 20250915164111.png]]

Usage of these estimators can form the *Data Pre-processing Pipeline*.

SciKit Learn Data Imputation:
Consider the following array of data:
```
array([[ 1.,  2., nan,  4.],
       [ 5.,  6., nan,  8.],
       [10., 11., 12., nan]])
```
```Python
# impute missing values via the column mean using sklearn's SimpleImputer

from sklearn.impute import SimpleImputer
import numpy as np

imr = SimpleImputer(missing_values=np.nan, strategy='mean')
imr = imr.fit(df.values)
imputed_data = imr.transform(df.values)
imputed_data
```
SimpleImputer takes as input the missing values identified here as "NAN" and imputes them using a specified strategy, which in this case is the *mean*. The default missing value identifier is NAN, but other datasets can have a variety of ways to represent a missing value (-999, 0, or -1)
The result we obtain is:
```
array([[ 1.,  2., 12.,  4.],
       [ 5.,  6., 12.,  8.],
       [10., 11., 12.,  6.]])
```
*Note*: When working with Scikit Learn, the output is always a Numpy array. 
We can also use Pandas:
```Python
# impute missing values via the column mean using pandas
df.fillna(df.mean())
```

Using One-Hot Encoding in Scikit Learn:
```Python
from sklearn.preprocessing import OneHotEncoder

X = df[['color', 'size', 'price']].values
print("X:\n",X,"\n")
color_ohe = OneHotEncoder()
xfirst=color_ohe.fit_transform(X[:, 0].reshape(-1, 1)).toarray()
print("X's first column after using OneHotEncoder:\n",xfirst,"\n")
```

```
X:
 [['green' 'M' 10.1]
 ['red' 'L' 13.5]
 ['blue' 'XL' 15.3]] 

X's first column after using OneHotEncoder:
 [[0. 1. 0.]
 [0. 0. 1.]
 [1. 0. 0.]] 
```

*Note:* we use dummy variables or one-hot encoding, we want to remember to drop a column! In linear systems, we cannot keep all dummy variables. This dropped feature will be a reference feature will be the feature against which the other features in the data are being measured against. 
In Pandas, by default, no indicators will be dropped. We can change this directly by including the `drop_first=True` argument.

## Overfitting 
How do we solve?
- MORE DATA: we tend to control overfitting, but it has limitations. 
- TUNE PARAMETERS: specifically the *hyperparameters*:
	- These are the parameters that have to do with how we train the model (learning rate is one of them)
- REGULARIZATION: reduce the sensitivity of a high variance model to each data point. If we have lots of features in our prediction, some of the features may be highly correlated, this may lead to a certain amount of overfitting. (Reduction of Coefficient):
- ![[Pasted image 20250915173427.png]]
	- #Regularization: **Add a penalty term to the error function to discourage learning a more complex model by forcing the model parameters to be small.**
	How do we decide which coefficients need to be shrunk?
	

We have our cost function: $$J = \frac{1}{2m}((Xw-y)^T(Xw-y)) + \frac{\lambda}{m}||W||^2_{2}$$
Lamba is a hyperparameter. 
Recall that ||w||<sup>2</sup> is W<sup>T</sup>W, which is just the L2 Norm. 

This is known as #RidgeRegression, where we are trying to "find the ridge" as easily as possible. 

An alternative form of this added penalty is:
$$+ \frac{\lambda}{m}||w||_{1} \leftarrow \sum^{m}_{j=1}|w_{j}|$$
Which is *L1 Regularization*, also known as #LASSO - “Least Absolute Shrinkage and Selection Operator.” Lasso solves a number of the issues that Ridge regularization in terms of dealing with outliers. However, the main problem with this form is that the absolute value function of |W| is non-differentiable at 0. We instead have to compute a sub-gradient. 

Yet another form exists: #ElasticNet

