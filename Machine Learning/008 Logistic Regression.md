## Logistic Regression 
#logisticregression
Classification using a different architecture, which is actually the linear model that we were using at the start of the course. 
• Connectionism  
• Logistic Regression  
	– Learning Logistic Regression  
	– Gradient Descent  
	– Regularization  
• Multinomial Logistic Regression

Recall the original process:
![[Pasted image 20250929174617.png]]
We have vector `x = [x1, x2, ..., x_m]`
And a scalar `h = summation(x_i + w_i + b)`
`= w^T * x + b`. *h* computes the dot product of inputs and the weights plus the bias. 
$$g(h) = g(\vec{w}^{T}\vec{x} + b)$$
(see notes)
One example of a function we could use for *g* is the **Sigmoid Activation Function**. The sigmoid function takes a real value and maps it to the range [0,1]. Because it is  
nearly linear around 0 but has a sharp slope toward the ends, it tends to squash  
outlier values toward 0 or 1.
Think about it in terms of *neurons*. It is either firing or not firing. We could not use the old linear model for classification because th output is unbounded. The activation function allows us to create lower and upper bounds of 0 and 1. This is convenient because we could equate this output value as a *probability*. 
$$\hat{y} = P(y=1|x)$$ $$1-\hat{y}=P(y=0|x)$$
$$P(y=1|x) = g(h) = \frac{1}{1+e^{-h}} = \frac{1}{1+e^{\sum^{m}_{i=1}w_{i}x_{i}+b}}$$
What we have then is the following:
$$h = w^Tx + b$$ $$\hat{y} = \frac{1}{1+e^{-h}} = sigmoid(h)$$
**Learning Logistic Regression**
• How are the parameters of the model, (the weights and bias) learned?  
• You guessed correctly:  
	✓ We set up an architecture  
	✓ We define a cost function  
	✓ We compute the gradient of the cost function  
	✓ We either derive a closed solution, if it exists, or use gradient descent

We have the problem of *nonlinearity*. The function we are using is not convex (when graphed, it is not a nice bowl shaped line). We are in a situation where we may find ourselves in a **local minimum**, which means that we need to change the kind of cost function that we are using:

This function is called the **Cross-Entropy** loss function. 
$$\hat{y} = P(y=1|x)$$ $$1-\hat{y}=P(y=0|x)$$
There is a more elegant way of writing the above expressions:
$$P(y|x) = \hat{y}^{y} * (1-\hat{y})^{1-y}$$
Therefore, if `y=1`, then we will just get `yhat`, and if `y=0`, then we just get `(1-yhat)`
If we take logarithms, we obtain the loss function:
$$L(y,\hat{y})=-y\log(\hat{y})-(1-y)\log(1-\hat{y})$$
This is convex, so it works much better. 

![[Pasted image 20251001093206.png]]
$$h=w^Tx + b$$$$\hat{y} = \frac{1}{1+e^{-h}} = sigmoid(h)$$
If `P(y = 1 | x) = yhat` then `P(y = 0 | x) = 1 - yhat`
We more elegantly wrote this as: $$P(y|x) = \hat{y}^y (1-\hat{y})^{(1-y)}$$
Overall, we will have:
$$\begin{bmatrix}
h
\end{bmatrix} = 
\begin{bmatrix}
X
\end{bmatrix} *
\begin{bmatrix}
W
\end{bmatrix}
+\begin{bmatrix}
b
\end{bmatrix}*1$$
`h: 1xm, X: mxm, w: mx1, b:mx1`
$$\vec{h} = X^T * \vec{w} + b \vec{1}$$
$$\begin{bmatrix}
\hat{y}
\end{bmatrix} = \begin{bmatrix}
sigmoid(h)
\end{bmatrix}$$
Each of the elements of `yhat` is computed as the sigmoid of h_1, h_2, h_3, over the observations. 
$$\hat{y} = sigmoid(\vec{h})$$
Now we need to generalize this loss function for all of the data. #Likelihood #CrossEntropy
In a similar manner as in our Bayesian learning data, each data point is contributing some probability. Remember:
$$P (data | x) = P(y_{1}|x) * P(y_{2}|x) * \dots *P(y_{n}|x)$$This product is called a **likelihood**, gathering all of the probabilities from all the data points. 
$$= \prod^{m}_{i=1}\hat{y}_{i}^{y_{i}}(1-\hat{y}_{i})^{1-y_{i}}$$
- Take logs 
- Change sign 
- Average over *m*

By taking logs, we are transforming the product expression into a sum of the terms:
$$J(w, b) = -\frac{1}{m}\sum^{m}_{i=1} y^{(i)}\log \hat{y}_{(i)} + (1-y^{i})\log(1-\hat{y}_{{(i)}})$$
The above first term of the expression is a *dot product*.
$$J(w,b) = -\frac{1}{m} \begin{bmatrix}
y\log \hat{y}+(1-y)^T\log(1-\hat{y})
\end{bmatrix}$$
We cannot find an analytical solution to this due to the nonlinearity. We will use gradient descent like with vanilla linear regression:
$$\begin{bmatrix}
w \leftarrow w - \eta/ \frac{\partial J}{\partial W}
\end{bmatrix},
\begin{bmatrix}
b \leftarrow w - \eta/ \frac{\partial J}{\partial W}
\end{bmatrix}$$
We need to compute the partial derivative of our cost function J w.r.t. the weights W.
$$\frac{ \partial J }{ \partial W } = \frac{ \partial J }{ \partial \hat{y} } * \frac{ \partial \hat{y} }{ \partial h } * \frac{ \partial h }{ \partial w } $$
Going one by one:
$$\frac{ \partial J }{ \partial \hat{y} } = -\frac{1}{m}\begin{bmatrix}
\frac{y}{\hat{y}}-\frac{(1-y)}{1-\hat{y}}
\end{bmatrix}$$
$$\frac{ \partial \hat{y} }{ \partial h } = \hat{y} \otimes (1-\hat{y})$$
$$\frac{ \partial h }{ \partial w } = X$$
Computing the product of all of this:
$$= \frac{1}{m}X^T(\hat{y}-y)$$ This is our gradient for linear models, exactly the same formulation. This is the average of the dot product of the data times the error. Doing this for *b* gives us simply: $$\frac{ \partial J }{ \partial b } = \frac{1}{m}(\hat{y}-y) $$This gives us all that we need to do computations. 

## Regularization 
#regularization is needed here comparatively more. 
$$J^{reg}(w,b) = J(w,b) + Reg[L_{1} or L_{2}]$$
$$L_{1}: \frac{\lambda}{m}|w|$$
$$L_{2}: \frac{\lambda}{2m}||w||^2$$
By penalizing the weights, we are shrinking the coefficients. This shrinkage of the weights allows us to prevent **overfitting**, as we saw earlier in the course. 



