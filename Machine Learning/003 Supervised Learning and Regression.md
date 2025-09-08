*Problem:* how to improve the sales of a given product 
*Data*: advertising data set consisting of the sales of the product in 200 different websites. This comes from 3 sources of advertising: TV, radio, and newspaper. 
*Goal*: develop an accurate model that can be used to predict the sales on the basis of those 3 markers. 

![[Pasted image 20250908153844.png]]

This is supervised learning:  
1. Collect training data  
2. Use a learning algorithm to fit a model  
3. Use model to make a prediction

![[Pasted image 20250908153922.png]]
The advertising budgets are  
input variables while sales  
input is an output variable.  
✓ Sales= f(Radio, TV ads )

We assume that there is some relationship between the output variable 𝑦 and the input variables denotes as a vector 𝐱 = (𝑥<sub>1</sub>, 𝑥<sub>2</sub>, . . , 𝑥<sub>𝑚</sub> which can be written in the very general form.
𝐱 represents the possible media sources, which = 3

	y = f(x) + e

Why *"+ e"*? We have a target and some fixed formula on that target to produce a solution, but perhaps we have some errors or missing data. Perhaps we need more variables or components in our vector 𝐱 to fully determine the function. We need some variation to take this into consideration. 

- *f* is fixed but unknown function of 𝐱.
- Assume error represents some noise with some variance. 
- *f* represents the systematic information that x provides about y. 
- However, *f* is **generally unknown**.
- In this case, one must estimate *f* based on the observed points. 

![[Pasted image 20250908154630.png]]

We fit *f*^(x;D) as the best possible by minimzing the mean squared error (MSE)
![[Pasted image 20250908155000.png]]
This kind of measure is a **cost function**. 
This is trying to measure the error between all the data points and the model attempting to predict *y<sup>^</sup>*. 
![[Pasted image 20250908155945.png]]

## Regression and Prediction
In any supervised model that we develop, we will train the model on some dataset that we have collected, but will always try to set aside a certain portion of the original dataset to be used for *testing purposes*.
This is the general idea of **splitting the data**.

We want the 𝑴𝑺𝑬 to be minimal for dataset 𝑫 (to find  
the best fit) and points outside the sample (in the latter,  
for accurate prediction purposes)

This means that we minimize 𝑀𝑆𝐸 on training data D to  
optimize the fit, and assess the effectiveness on points  
outside the sample by computing 𝑀𝑆𝐸 on test data (same  
formula, different dataset)![[Pasted image 20250908160116.png]]

This is to ensure that the model is capable of *generalizing* its predictions beyond the data it has been presented. 

**Two Sources of Erorr in our Prediction**
Of course, we cannot hope to fit the function perfectly to y, since 𝑦 = 𝑓(𝐱) + 𝑒 contains noise e.
Even if we were to form a perfect estimate for *f*, so that the estimated response took the form y^ = f^(x), our prediction would still have some error!
	y is also a function of error e, which, by definition, cannot be predicted using x. 
	Therefore, variability associated with e also affects the accuracy of our predictions. This is known as the #irreducible error.
Also, f^ will not be a perfected estimate for *f*, and this inaccuracya will introduce some error. This is known as #reducible error.
The accuracy of 𝑓(𝐱;𝐷) as an estimate for 𝑦 therefore depends then on two quantities, the reducible error and the irreducible error.
![[Pasted image 20250908160318.png]]
Two important points to consider: **bias** and **variance**. 

![[Pasted image 20250908161159.png]]

The irreducible error is given by the Variance of the noise The reducible error is given by the expectation of the squared difference between f^(𝐱) and y<sup>^</sup>.
Consider the *expected value* given by E[...] as an average. 

Useful derivation explanation:
![[Pasted image 20250908161939.png]]
var(e) will be our irreducible error, but without knowing exactly how to measure it. 
- We have found that the expectation of the observation minus the estimation, squared = var(e) + E[(f(x)-y^)^2] as shown above. 

**Assessing Model Accuracy**
How can we measure how close y is getting to f? 
![[Pasted image 20250908162349.png]]
![[Pasted image 20250908162402.png]]

Suppose we have: 
Simple Linear regression: $$y = w0 + w_{1}x$$
A cubic polynomial: $$y = w_{0} +  w_{1}x + w_{2}x^2 + w_{3}x^3$$
A polynomial of degree 10: $$y = w_{0} + \sum^{10}_{o = 1} w_{o}x^o$$
Of course, complexity increases as the degree gets higher. 

**Overfitting and Underfitting**
![[Pasted image 20250908163403.png]]

If a model has low bias and very high variannce, it can be said to have low generalizability, where the model cannot predict well when given new data.

![[Pasted image 20250908163108.png]]
![[Pasted image 20250908170712.png]]
![[Pasted image 20250908170906.png]]

How we can visualize training error reduction via **regularization**- shrinking the added complexity that we have in the models. 
- This looks at higher degree polynomials
- Things that naturally possess high variance
![[Pasted image 20250908170943.png]]
# Linear Regression 
#Regression
Machine Learning is Optimization 
1) Given a certain problem, choose some *ARCHITECTURE*.
	This may be a decision tree, a linear model, a neural network, a group of trees working together, an ANN/CNN algorithm, etc. 
2) *TIED TO THE TASK*, *DEFINE THE OPTIMIZATION MODEL*.
	Our optimization model means the following:
	- Find some mechanism to measure the loss function. 
	- The loss function is tied to the task, not the same across problems.
	- $$L = \frac{1}{2}(\hat{y} - y)^2$$
	- For m points -> J: $$ \frac{1}{2n} \sum^{m}_{j = 1}(\hat{y}^i - y^i)^2$$
3) *CHOOSE SOLUTION* (can be numerical or analytical)
4) *VECTORIZE* 
	Makes things far more elegant, and in terms of the packages we use, they vectorize everything. 
5) *EMIGRATE*

## Linear Regression 
Define the architecture: 
$$LR: y=f(x) + e \to \hat{y} = \sum^{m}_{j = 1}w_{j}x_{j} + b$$
This is the general expression, but this does not take into account our dataset. *y* is merely a function of the vector **x**, which is {x<sub>1</sub>, x<sub>2</sub>,..., x<sub>m</sub>}<sup>T</sup> 


