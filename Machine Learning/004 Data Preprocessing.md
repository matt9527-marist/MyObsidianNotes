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

