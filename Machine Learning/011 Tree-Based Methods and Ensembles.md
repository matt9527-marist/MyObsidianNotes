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

**Recursive Splitting**
> FOR each x in X
> 	FOR each split ts in xi 
> 		Keep the pair(xi, ts) that minimizes J, a cost function 
>* Recursively grow the tree until stopping criterion

In the case of regression, we usually use some cost function of a quadratic loss.
$$SSE_{R_{1}} + SSE_{R_{2}} + \dots$$
Minimize the sum of squared errors on the left of the split and on the right of the split, and on the top of the split and on the bottom of the split. 
This will allow us to find the best possible pair to place a split across all possible pairs. 
How many times will we repeat the selection process?
- Stopping Criterion: set count of times, or a specific condition. 
	- Why can't we let the tree continuously grow? Remember training vs. testing error. We do not want overfitting. 

Decision trees are very popular for two reasons:
1) Recursive situations over a lot of attributes. Combinatorial explosions like this are handled relatively quickly by modern computers. 
2) The tree by itself is a graphical representation of a collection of rules. Just a few thousand conditional branches checking the values of attributes. 
One big problem: This algorithm has extremely low bias and very high variance. When the tree grows, it is essentially adding more and more rules. The tree *grows aorund the data*. 
Can be affected by random state starts. 
- What to do? Start cutting branche (reducing ruleset), called pruning. 

We need a cost function. If it is regression, we can use sum of square errors on the left side of the split (R1) + sum of the square errors on the right side of the split (R2).
Find `xi*, ts*` that minimizes `J`

What do we do in classification? We do not have the sum of square errors or a quadratic form of loss. The researchers who developed CART use the metric: 
Classification: ***Impurity Metric***: 
(see notes)
How do we make the determination that the above split `t1` is the best one?
Use the *Gini Index*:
$$Gini = \sum^{k}_{k=1}p^{k}(1-p_{k})$$
We could have a target that contains up to `k` classes. In the case above, `k=2` classes. 
`P(closed) = 6 / 11`
`P(open) = 5/ 11`
What is the probability of misclassification? For example, predicting an open (6/11). 
Another way of writing this:
$$G =  (1-\sum^{k}_{k=1}p_{k})^2$$
How can we measure the improvement by splitting? 
We use the Gini for the above situation: 
$$G = 1 - [(\frac{6}{11})^2 + (\frac{5}{11})^2]$$
After we split this:
$$G_{R_{1}} = 1 - [(\frac{2}{5})^2 + (\frac{3}{5})^2]$$
$$G_{R_{2}} = 1 - [(\frac{2}{6})^2 + (\frac{4}{6})^2]$$
We go from 1 Gini Index to 2 Gini Indexes after the split. Next step is take the average: 
$$\bar{G_{R_{1}, R_{2}}} = \frac{N_{R_{1}}}{N}G(R_{1}) + \frac{N_{R_{2}}}{N}G(R_{2})$$
$$= \frac{5}{11}G(R_{1}) + \frac{6}{11}G(R_{2})$$
This gives us our *improvement*. We start with a level of impurity for the full box before splitting. Because we split, we have less impurity in the regions. 
$$G - \bar{G_{R_{1},R_{2}}}$$
We could have placed a split that gives certainty for one data point, but it would be one-sided. For each potential split `ts` that the system considers, the system will compute the SSE for the right and left sides of the split for regression, or compute the improvement for classification. 

Another metric is **entropy**: $$H = -\sum^{k}_{k=1}p_{k}\log p_{k}$$We owe this to Claude Shannon. This is an information theoretical metric, a measure of uncertainty associated with a random variable. 

Suppose we perform a mapping of a small alphabet to prefix codes: 
(see notes)
Why would we prefer the left side mapping? We know that the letters `A` and `E` are very common. If `A` appears 8% of the time, and `E` appears 13% of the time vs. `Q` and `Y` appearing 0.1% and 2% of the time, we want *shorter prefix codes* for `A` and `E`. 

**Information Gain**
Coming from thermodynamics, we know that in any closed system, entropy always increases. If entropy always increases, we have a gain in information. 
Organized the same way as computing the Gini Index. 

## Ensembles 
Intuition: If we have to make a prediction about something, would we ask the person next to us or the whole class? Why not use an *ensemble* of estimators instead of just one? 
--> No Free Lunch Theorem (NFL):
- If we average all possible problems, there is no single estimator that performs better than the rest. 
- Consequences: there may be some algorithms that are better for certain problems than others, but it is difficult to identify the best possible algorithm. We cannot possibly try every algorithm. 
- If we take a group of algorithms, it may be better off, since there is no best singular algorithm. 

