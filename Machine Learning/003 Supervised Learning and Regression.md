## Supervised Learning
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
#Regression #LinearRegression
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

We have a dataset D and prediction y, vectorized as:
![[Pasted image 20250908173102.png]]
This gives us: $$\hat{y} = W\vec{x} + b_{\vec{1}}$$
We now need to present the cost function:
$$ J(w, b) = \frac{1}{2m}\sum^{m}_{i=1} (\hat{y^i} - y^i)^2$$
This is a *dot product*. 
We can rewrite this in the following way:
$$= \frac{1}{2m}(\hat{y}-y)^T(\hat{y}-y)$$
$$J(w,b) = \frac{1}{2m}(X\vec{w}+b - y)^T(X\vec{w} + b -y)$$
In order to discover the minimum of our cost function, need to find:
$$\frac{ \partial J }{ \partial w }  = 0$$
Therefore consider:
$$j = \sum^{m}_{i=0}w_{j}x_{j}$$
$$\begin{bmatrix}
x_{1}^1 \dots x_{m}^1 \\ \\
\dots \\
x_{n}^1 \dots x_{m}^n
\end{bmatrix} \begin{bmatrix}
w_{0} \\
w_{1} \\
\dots \\
w_{m}
\end{bmatrix}$$
$$\hat{y} = Xw$$
$$J(w) = \frac{1}{2m} (\hat{y}-y)^T(\hat{y} - y)$$
$$= \frac{1}{2m}(Xw-y)^T(Xw-y)$$
Compute the derivative wrt. *w* of *J*:
Assume that we have a variable:
$$\mu = (Xw -y)$$
Using this variable:
$$\frac{d(J)}{dw} = \frac{d(\mu^T\mu)}{dw} = 0$$
What is this?
- This is the derivative of a scalar by a vector.
![[Pasted image 20250908174954.png]]
Recall the 3 rules: this is the last one. The derivative of a vector with respect to a vector. 
![[Pasted image 20250908175150.png]]
Notice step 3: this is the chain rule- the derivative of a function f(g(x)).
Notice also that we must respect the rule to lay out the numerator in columns and the denominator in rows. This computation respects this by transposing the result.
We obtain through derivation:
$$\frac{dJ}{dw} = \frac{d\mu^T\mu}{dw} = 2(\frac{d\mu}{dw})^T \bullet \mu$$
Which has to be equal to 0 in order to minimize it.
Recall: $$\mu = Xw-y$$
$$ = 2 [\frac{d}{dw}(Xw-y)]^T \bullet (Xw - y) = 0$$
$$X^T \bullet (Xw-y)=0$$
$$X^TXw - X^Ty = 0$$
$$X^TXw = X^Ty$$
Finally, finding the equation for w: $$w = (X^TX)^{-1}X^Ty$$
This equation represents the analytical solution, but it may not solve the problem accurately if the matrix is very large. 

What does this look like in Python?
```Python
def calc_normal_eq(x, y):
	n, m = np.shape(X)
	XTX = np.dot(X.T, X)
	XTX_1 = np.linalg.inv(XTX)
	XTy = X.T @ y
	return XTX_1 @ XTy
```
Be careful: inverting a matrix of 500 by 500 features is probably not the best idea. 
The product is never an issue computationally. 

## Gradient Descent 

#gradientDescent 
We need some numerical approach that allows us to approach the minimum point over the course of some iterations. 
$$w_{new} = w_{old} + \triangle w$$
$$w_{new} = w_{old} - \eta\nabla J$$
Take the following situations:
![[Pasted image 20250908181222.png]]
![[Pasted image 20250908181230.png]]
The rule *eta* is what is referred to as a *hyperparameter*. This value can allow us to control the rate at which we increase or decrease w. 

![[Pasted image 20250910105855.png]]
	
**How do we know that this algorithm works?**
![[Pasted image 20250910105823.png]]

## Linear Regression Colab

[Linear Regression Notebook](https://gist.github.com/eitellauria/d078daf59337462b81caf51c9511b20d)

```Python
from sklearn.datasets import fetch_california_housing

# Note that by selecting as_frame=True, that data is placed in a pandas DataFrame

california_data = fetch_california_housing(as_frame=True)

print(california_data['DESCR'])
```

**SkLearn**, or **Scikit Learn** has many sample datasets that we can fetch from. This is a tool serving as a machine learning library. 
This particular California housing dataset specifies the target as the value of the house, which we want to predict according to the set of available features. 

```Python
# we will only work with two of the features: MedInc and AveRooms

X = df[['MedInc', 'AveRooms']].values

y = df['MedHouseVal'].values
```

Two columns for the time being, we want to extract our **X** and y. In this case, m = 2 variables to consider in making predictions. 
**Define the Cost Function**
  

$$J(\textbf{w}) = \frac{1}{2n} \sum_{i=1}^n (\hat{y}^{[i]}-y^{[i]})^2 $$

$$J(\textbf{w}) = \frac{1}{2n} \sum_{i=1}^n (w_1 x_1^{[i]} + w_2 x_2^{[i]} + b -y^{[i]})^2 $$
This is what we are going to use, but this is with summations. In code this looks like the following:

```Python
def cost(w1, w2, b, X, y):
    '''
    Evaluate the cost function in a non-vectorized manner for
    inputs `X` and targets `y`, at weights `w1`, `w2` and `b`.
    '''
    costs = 0
    for i in range(len(y)):

        yhat_i = w1 * X[i, 0] + w2 * X[i, 1] + b

        y_i = y[i]

        costs += 0.5 * (yhat_i - y_i) ** 2

    return costs/len(y)
```

**Vectorizing the Cost Function**
$$J(\textbf{w}) = \frac{1}{2n} ( \bf{X} \bf{w} + b \bf{1} - \bf{y} )^T(\bf{X} \bf{w} + b \bf{1} - \bf{y} )$$
 $$=\frac{1}{2n} \| \bf{X} \bf{w} + b \bf{1} - \bf{y} \| ^2$$

Vectorized, this is what it looks like in the following code:

```Python
def cost_vectorized(w1, w2, b, X, y):
    '''
    Evaluate the cost function in a vectorized manner for
    inputs `X` and targets `y`, at weights `w1`, `w2` and `b`.
    '''
    n = len(y_train)
    w = np.array([w1, w2])
    yhat = np.dot(X, w) + b * np.ones(n)
    return np.sum((yhat - y)**2) / (2.0*n)
```
Note: this is NOT the augmented version from earlier where we omit "+b"

**Closed Form Solution**
The optimal vector of weights $\textbf{w}=(\bf X^TX)^{-1}X^Ty$
where $\textbf{w}$ includes $w_0 \equiv$ bias $b$ and $\bf X$ is augmented with a first column  of 1s.
1. ignore biases (add an extra feature & weight instead)
2. get equations from partial derivative
3. vectorize
4. write code

We need to do some work beforehand. We add an extra feature (new column) of just ones to X. 

```Python
def solve_normal_eq(X, y): # Using @ operator
    '''
    Solve linear regression exactly. (fully vectorized)

    Given `X` - n x m matrix of inputs
          `y` - n x 1 target outputs
    Returns the optimal weights as a m-dimensional vector
    NOTE that I use the @ operator instead of the np.matmul function.
         It yileds a cleaner syntax
    '''
    n, m = np.shape(X)
    
    XTX = X.T @ X
    XTX_1=np.linalg.inv(XTX)
    XTY=X.T @ y
    return XTX_1 @ XTY
```
(Using the @ operator, as opposed to .matmul, which is for matrix multiply)
```Python
w = solve_normal_eq(X_train_aug, y_train)
for i in range(len(w)):
  print(f'w{i}={w[i]:.5f}')
```
This printing statement is convenient for formatting. Be sure to use [f'...'] expressions to be more clean in presentation. 
**Scikit Learn** has its own way of *fitting* the models to data. It has Linear Regression. We can compare our results to this function that is already available in the library:
```Python
# For comparison, this was the exact result:
from sklearn.linear_model import LinearRegression

reg = LinearRegression().fit(X_train, y_train)
print(f'intercept={reg.intercept_:.5f}')
for i in range(len(reg.coef_)):
  print(f'w{i+1}={reg.coef_[i]:.5f}')
```

We can now begin with a simple linear regression function to make predictions on our testing data X_test. 
```Python
def linreg(w,b, X):
  return np.matmul(X,w) +b
  
b=w[0]
w1=w[1]
w2=w[2]

y_pred = linreg(np.array([w1,w2]),b,X_test)
print(y_pred)
```
We can also of course do this with the SkLearn.predict method. 

## Gradient Descent Colab

[Gradient Descent](https://gist.github.com/eitellauria/b09d3b953c56a84e984802294d5b937b)

Implement Gradient Descent

$$ \frac{\partial J}{\partial w_j} = \frac{1}{n}\sum_i x_j^{[i]}(\hat y^{[i]}-y^{[i]}) $$

$$ \frac{\partial J}{\partial w_j} = \frac{1}{n}\sum_i x_j^{[i]}(\sum_{j=0}^m w_j x_j^{[i]}-y^{[i]}) $$

$$ w_{new} \leftarrow w_{old} - \eta \frac{\partial J}{\partial w_j} $$

Vectorizing the formulation:

  

$$ \nabla J(\bf{w} )  = \mathrm{\frac{1}{n}}\bf{X}^T(\hat{y}-y)$$

$$\textrm{with } \bf\hat{y}=X \bf{w}$$

$$\textrm{so } \bf{w}^{(new)}← \bf{w}^{(old)}-\eta   \nabla J(\bf{w})$$

$$\textrm{that is  } \bf{w}^{(new)}← \bf{w}^{(old)}-\eta\mathrm{\frac{1}{n}}\bf{X}^T(\hat{y}-y)$$
With these equations, we obtain this function:
```Python
# Vectorized gradient function
def gradfn(weights, X, y):
    '''
    weights: a current "Guess" of what our weights should be
          X: matrix of shape (n,m) of input features
          y: target y values
    Return gradient of each weight evaluated at the current value
    '''
    n, m = np.shape(X)
    
    yhat = X @ weights
    error = yhat - y
    return (np.transpose(X) @ error)/float(n)
```
We can then use this to solve:
```Python
def solve_via_gradient_descent(X, y, print_every=100000,
                               niter=1500000, eta=0.005):    
                               #Try large values of iterations !
    '''
    Given `X` - matrix of shape (N,D) of input features
          `y` - target y values
    Solves for linear regression weights.
    Return weights after `niter` iterations.
    '''
    n, m = np.shape(X)
    # initialize all the weights to random values
    w = np.random.rand(m)
    for k in range(niter):
        dw = gradfn(w, X, y)
        w = w - eta*dw
        if k % print_every == 0:
            print (f'Weight after {k} iteration: {str(w)};  
            gradient: {str(dw)}')
    return w
    
w=solve_via_gradient_descent( X=X_train_aug, y=y_train)
print('\n')
for i in range(len(w)):
  print(f'w{i}={w[i]:.5f}')
```

## Stochastic Gradient Descent 
When we refer to SGD, 
$$w_{new} = w_{old} - \eta \nabla J(w)$$
$$J = \frac{1}{2n}(Xw-y)^T(Xw-y)$$
All of the terms above are vectors. 
$$\nabla J = \frac{1}{n}X^T(Xw-y)$$
At each pass, we are going over the full dataset. This has a *cost*, not much if it is simple regression, but to compute each `w` we are looking at all of the data again. This means a lot of iterations. 

Instead of using the full `X`, we may use minibatches of `X`, extracted at random from the data. If we do this, we also need to pull the initial `y` values. With this, we will have a much smaller set of data with which to update the `w`'s. 

We compute the gradient against the minibatch. 

SGD guarantees a local minimum. It does need a bit more of a push to reach the global minimum. This is good for #LinearRegression. For more complex models, we might need to help SGD a certain amount. 