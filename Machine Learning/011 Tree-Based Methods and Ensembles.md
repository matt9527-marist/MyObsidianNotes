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
#Ensembles
Intuition: If we have to make a prediction about something, would we ask the person next to us or the whole class? Why not use an *ensemble* of estimators instead of just one? 
--> No Free Lunch Theorem (NFL):
- If we average all possible problems, there is no single estimator that performs better than the rest. 
- Consequences: there may be some algorithms that are better for certain problems than others, but it is difficult to identify the best possible algorithm. We cannot possibly try every algorithm. 
- If we take a group of algorithms, it may be better off, since there is no best singular algorithm. 

Imagine the following situation:
(see notes)
Suppose each of the above lines is one linear classifier. On their own, they have a lot of errors, but when we use them together, we get much better results. 

**Types of Ensembles**:
1) Homogeneous: Trees are the same
	- Decision tree ensembles: Bagging, Boosting, 
2) Heterogeneous: Stacked Estimators: Trees are different
	- Variants of Bagging: Random Forests (RF), Extra Trees

Example ensemble usage using decision trees:
(see notes)
Essentially breaking the initial dataset D into a set of datasets organized in a tree, where we can use multiple decision trees for each division. 
$$X \to \frac{x_{1}, x_{2}, \dots x_{B}}{\bar{x}}$$
$$var(\bar{x}) = \frac{\sigma}{B}$$
One problem: the trees are highly correlated. We may have hundreds of estimators, but perhaps the majority of them look very alike because some features are more relevant than the rest. 
How can we fix this? This brings us to Random Forests.

**Random Forests**: Keep the structure, but extract at random a subset of the features to be used in each of the splits. By doing so, the correlation among trees disappears. The same feature that appeared at the top of trees beforehand may not be used. The value of how many features to select is a hyperparameter, and it can be chosen at random. 
*Random Walk*: Assuming we use no logical criterion to produce a split. At random, choose a set of features and produce a split with them. 

#Boosting
**Boosting**: adaptive algorithm that reduces the error due to both variance and bias. Focuses on training examples that are hard to classify. 
- Sequentially build newer and newer weak learners. Each learner learns from the one before. 
- This is as opposed to *bagging* which aggregates all the learners in parallel. 
Trees are grown sequentially. 

**Boosting Algorithm**
Given the training data `xi, yi`, number of trees `B`, and the shrinkage parameter `lambda`, and tree depth `d`.
1. Initialize the model:
   f(xi) = 0, ri = 0 
   `ri` is the residual (difference between `y` and `yhat`)
2. For each iteration: 
   Compute the fitted values of the tree for each observation (fitted on the residuals).
   $$T_{b}(x_{i})=r_{i}^{b}$$
   Update the model incrementally:
   $$f^{(b)}(x_{i}) = f^{(b-1)}(x_{i}) + \lambda T_{b}(\xi)$$
   Our new prediction is based on our previous prediction + the fitted tree on the residuals
   Update the residuals again:
   $$r_{i}^{b}=y_{i} - f^{b}(x_{i})$$
   These new residuals represent what is still left to explain. 

How many times do we boost the trees? Stop after a given number of iterations or after some criterion (for example until the error MSE reaches a threshold)
If we, at each stage compute a new prediction, we are creating a sequence of trees. 
$$f^{(B)}(x) = \sum^{B}_{b=1}\lambda T_{b}(x)$$
**Boosting Methods**
• Adaboost: originally formulated by Freund and Schapire in 1997, became  
one of the most widely used ensemble methods in the years that  
followed. https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.32.8918  

• Gradient boosting: (Friedman 2001). A variation of Adaboost,  
generalizing it by allowing optimization of an arbitrary differentiable loss  
function. https://statweb.stanford.edu/~jhf/ftp/trebst.pdf  

• XGBoost (Chen and Guestrin, 2016): A variation of gradient boosting.  
Probably the best performing supervised learning algorithm when applied  
to structured data. https://arxiv.org/abs/1603.02754  

**Gradient Boosting**: fit the model, in a generalized matter, not necessarily on the residuals, but fit the data on the *negative gradient* of a chosen loss function with respect to, NOT the parameters, but current the predictors. 
![[Pasted image 20251022100948.png]]
The residual is just a special case of fitting our models on the -derivative of the loss with respect to the predictions. If we apply this to Cross Entropy, we get the same thing (very similar to Hinge Loss).
Insight: We are not just fitting on the residuals. What we are fitting is really on the (-gradient) of the loss with respect to the prediction at each stage. 

**Gradient Boosting Algorithm**
Sum of weak models sequentially. Each new tree corrects the errors made by the previous trees by fitting to the negative gradient of the loss function w.r.t. the current model predictions: 
$$\hat{f}^{(B)}(x) = \hat{f}^{(0)}(x) + \eta \sum^{B}_{b=1}T_{b}(x)$$
Key Insight: Do not compute the derivative of the tree itself, just the gradient with respect to the predictions. 
![[Pasted image 20251022101443.png]]