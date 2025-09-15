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
Consider the following data
```
array([[ 1.,  2., nan,  4.],
       [ 5.,  6., nan,  8.],
       [10., 11., 12., nan]])
```
