1) **Decision Trees (DT)**:  Classification and Regression Trees (CART)
2) **Ensembles**: do not necessarily have to be decision trees. 

*Decision Trees*: to be able to build an algorithm that allows us to create rules. 
A collection of predictors organized in a certain way, where we start on a root and are led to leaves, representing whichever prediction on a target we come up with. 

We will be organizing the predictors in a specific order. The set of branches leading to the leaves (predictions) are going to represent decision rules of the form:
> IF outlook = overcast 
> 	OR outlook = sunny 
> 		AND humidity = low --> play_tennis = YES

**Different types of trees**: ID3, C4.5, C5.x, CART, QUEST... 
