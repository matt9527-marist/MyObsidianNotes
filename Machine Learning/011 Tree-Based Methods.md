1) **Decision Trees (DT)**:  Classification and Regression Trees (CART)
2) **Ensembles**: do not necessarily have to be decision trees. 

*Decision Trees*: to be able to build an algorithm that allows us to create rules. 
A collection of predictors organized in a certain way, where we start on a root and are led to leaves, representing whichever prediction on a target we come up with. 

We will be organizing the predictors in a specific order. The set of branches leading to the leaves (predictions) are going to represent decision rules of the form:
> IF outlook = overcast 
> 	OR outlook = sunny 
> 		AND humidity = low --> play_tennis = YES

**Different types of trees**: ID3, C4.5, C5.x, CART, QUEST... 

How do we split DTs:?
- number of branches per split: 
	- Binary (CART)
	- Multiway (C4.5)
- Split criterion: 
	- CART can be both a classifier and a regression model, whereas C4.5 is more of a classifier. 

**CART**
(see notes)
Select a predictor and within the predictor itself, let us choose a split:
> FOR each x in X 

What we have done is specify two regions defined by `t1`, where `x1 <= t1`
We are taking the predictor `x` and determining a certain split on it. 
> FOR each split `ts` in `xi`

We can split again within the first region as we see with `t2`. This is what we see when we choose the predictor `x2`. What we are saying here is:
(see notes)

The region selection is not the prediction. The prediction comes from doing `yhat(Ri)`
`yhat(R1)`, in terms of regression, is just the mean of all of the values within R1. 
$$\hat{y} = mean(\hat{y}_{i \in R_{i}})$$

This is regression, but what would change if we want to do *classification*? 
Let's assume that the following is binary: 
(see notes)
Classification means to take the probability of the majority class:
$$\hat{y} = prob(\text{majority class})$$
This renders an interesting point: 
- It will render a class, but it will have attached probability coming from calculating the proportions. This can be seen as a probabilistic algorithm. 

> FOR each x in X
> 	FOR each split ts in xi 
> 		Keep the pair(xi, ts) that minimizes J, a cost function 

In the case of regression, we usually use some cost function of a quadratic loss.
$$SSE_{R}$$