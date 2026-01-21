A big issue that we typically have in machine learning is when we are dealing with datasets containing a lot of predictors. One example is gene expression, which is a problem that makes our dataset very wide in comparison to the number of observations that you can gather. 

This creates a number of issues:
- Why are we concerned about having too many dimensions?
	- Not only the number of observations that are required to come up with good estimates may not be sufficient 
	- High dimensional space is particularly *sparse*. Take a line with points on it. When you increase the dimension to 2D, the points will spread out more. In 3D, it will be even worse. 
![[Pasted image 20251103162500.png]]
- Suppose we wanted to compute the average distance between random points that uniformly distributed between 0 and 1. 
- This is computing the expectation $$E[d^2]$$
- Suppose we have two points A and B: $$E[(b-a)^2]$$$$E[x] = \int xf(x)dx$$where f(x) is the density function:
$$f(x) = \frac{1}{x_{2}-x_{1}}$$
Recall this works similarly to the product of probabilities of independent events. 
$$f(a,b) = f(a) * f(b) = 1 * 1 = 1$$
$$E[d^2] = E[(b-a)^2] = \int^{1}_{a}\int^{1}_{b}(a-b)^2[f(a,b)=1]dadb$$
$$= \frac{1}{6}$$
This means that the distance squared in 1D between two uniformly distributed random points is equal to 1/6. If we have n dimensions, we have `n * 1/6`.
The distance in n dimensions is given by:
$$d_{nD} = \sqrt{\frac{n}{6}}$$
For 2 dimensions, for example:
$$d_{2D}=\sqrt{ \frac{2}{6} } = 0.52$$
What happens if we are working within a space of one million dimensions? 
$$d_{10^6D} = \sqrt{ \frac{10^6}{6} } = 408.25$$
This indicates that we are operating within an extremely sparse space. We cannot work in such a space because the chances that we will be able to come up with a good estimate or find data in it is very difficult. 

## Principle Component Analysis
#PCA
![[Pasted image 20251103163616.png]]
How do we go from an initial dataset X to a dataset P, where the number of dimensions is `k` and is as much as possible `k < m`, a reduced number of predictors. 

One approach: Think about it in terms of photography. If we want to take a picture of an object, say a teapot, from what angle can we take a 2D image of the teapot to capture the full variation of the data? 

Suppose we have a 2D dataset:
(see notes)
We notice that the points lie on a specific axis. We can define `PC1` and `PC2`, which are linear combinations of `x1` and `x2`. 
We have gone from our original feature space (x1, x2) 2D space into principle component feature space. In this way, we can just choose to keep `PC1`. It represents 80-90% of the variation of the data. Keep in mind that no one uses PCA with just 2 variables. 

*PCA = Eigen Decomposition*

**Brief Detour (Statistics)**
Suppose we have `xj ... xj`, `xk ... xn`
The variance:
$$S^2_{j} = \frac{1}{m-1}\sum^{m}_{i=1}(x^{[i]}_{j} - \bar{x}_{j})^2$$
Compute the difference squared, added over all the observations, divided by `m-1`

The *covariance*: $$cov(x_{j}x_{k}) = \frac{1}{m-1}\sum^{}_{}(x^{[j]}_{j}-\bar{x}_{j})(x^{[i]}_{k}-\bar{x_{k}})$$
How much variance there is along a specific variable when it changes. 
We can place this into a matrix:
$$C = \begin{bmatrix}
S^2_{1} && cov(x_{1},x_{2}) \\
cov(x_{2},x_{1}) && S^2_{2}
\end{bmatrix}$$
This is more familiar to the *correlation coefficient*, a value between -1 and 1 that is measuring the linear relationship between two variables. 
Let us relate the correlation coefficient to the covariance:
$$r_{jk} = \frac{cov(x_{j},x_{k})}{s_{j} s_{k}}$$
$$= \frac{1}{m-1}\sum^{m}_{i=1}\frac{x^{[i]}_{j} - \bar{x_{j}}}{s_{j}}\frac{x^{[i]}_{k} - \bar{x_{k}}}{s_{k}}$$
Recall: the square root of covariance is the standard deviation `s`.
$$= \frac{1}{m-1}\sum^{m}_{i=1}z^{[i]}_{j} * z^{[i]}_{k}$$
$$R = \frac{1}{m-1}z^Tz$$
Recall: the dot product.
Important note: the covariance matrix is a square matrix. It is a positive definite matrix. This means it is special kind of square matrix with specific properties that will be relevant. 
It is also a symmetric matrix. 

The correlation matrix `R`:
$$R = \begin{bmatrix}
1 && r_{1,2} \\
r_{2,1} && 1
\end{bmatrix}$$
Along the principle diagonal, the value is 1 because the correlation coefficient of a value with itself is always 1. 

**Brief Detour (Linear Algebra)**
![[Pasted image 20251103172500.png]]
![[Pasted image 20251103172353.png]]
Given a vector `v1`:
v2 = A * v1 
What would happen if we are in a special situation: 
![[Pasted image 20251103172614.png]]
We start with a vector `v1` and we multiply it by a a value `lambda` that does not change the angle but increases its magnitude for `v2`.
$$v_{2} = \lambda v_{1} = A * v_{1}$$
$$A * v_{1} = \lambda * v_{1}$$
For a given square matrix, there are certain instrinsic characteristics of the matrix itself that give way to this:
- The matrix A has a collection of pairs `lambda` and `e` such that: $$Ae = \lambda e$$
- This needs to be solvable in this way:
$$(A - \lambda \mathbf{I}) * e = 0$$
$$\det(A-\lambda \mathbf{I}) = 0$$
These properties are intrinsic/proper to the matrix, and thy are called *eigenvalues* and *eigenvectors*, which represent the number of derived solutions from the equation above. (`lambda`, `e`)
The eigenvectors corresponding to distinct eigenvalues of a square matrix are *orthogonal*, meaning we can use them to produce that earlier dimensionality reduction. 

From a square matrix C, we can extract the eigenvalues `lambda` and eigenvectors `e`. 
If C is (m x m), we will extract m eigenvalues and eigenvectors. 

*Example*
Suppose we have X that is (n x m). We convert this to standard deviations (n x m) using the averages of the observations. We then convert this into PC (n x m) by doing PCA. 

`Z (n x m) features`
We have eigenvalues:
$$\lambda_{1}, \lambda_{2}, \dots \lambda _{m}$$
and eigenvectors:
$$\bar{e}_{1}, \bar{e}_{2}, \dots \bar{e}_{m}$$
(see notes)
$$R = \begin{bmatrix}
1 && r_{1,2} \\
r_{2,1} && 1
\end{bmatrix} \rightarrow \begin{bmatrix}
\lambda_{1} && 0  \\
0 && \lambda_{2}
\end{bmatrix}$$
The process of eigen decomposition will *diagonalize* `R`. 
Also important to remember:
$$\sum var(z) = \sum var(PC) = \sum \lambda_{j} = m$$
and remember:
$$\%var(PC_{j}) = \frac{\lambda_{j}}{\sum \lambda_{j}} = \frac{\lambda_{j}}{m}$$
As shown below:
![[Pasted image 20251103175057.png]]
![[Pasted image 20251103175131.png]]
All of this analysis is *linear*. If there is nonlinear variance, we cannot capture it, but it is still extremely useful to reduce dimensionality. 
*How many axes are needed?*
Just depends on how much of the variance that we want to explain. If we keep the PCs for which the eigenvalues >1, it does not mean we cannot choose a C where the eigenvlaue is 0.9 or 0.8. 
![[Pasted image 20251103175450.png]]

**PCA Overview**
![[Pasted image 20251105093922.png]]
If we have two variables, x1 and x2:
The correlation coefficient is given as: $$\frac{cov(x_{1},x_{2})}{s_{1}s_{2}} = cov(z_{1},z_{2})$$$$R(X) = C(z)$$
The correlation matrix is positive definite. That is, where `x^TAx > 0`. Where this is the case, the eigen decomposition will result in `lambas (eigenvalues) > 0`, and the eigenvectors will be orthogonal. Why is this interesting? 

This means we are creating a dataset that is uncorrelated. Correlations can often get in the way of explaining what influence a variable has on the results (this is in the case of social sciences for example). 

PCA = EIGEN DECOMPOSITION 
Generates [lambda{1} > lambda{2}, ...  > lambda{m}] 
and corresponding eigenvectors [v1, v2, ... v_m], all orthogonal to each other. 
Allows us to represent a matrix `V` of all the eigenvectors, ordered by the ranking of eigenvalues. 
$$PC_{1} = v_{11}z_{1} + v_{21}z_{2} + \dots + v_{m1} + z_{m}$$
$$\dots$$
$$PC_{m} = v_{1m}z_{1} + v_{2m}z_{2} + \dots + v_{mm}z_{m}$$
In terms of one observation. If we wanted it to be in terms of all observations, we would have:
$$\begin{bmatrix}
PC
\end{bmatrix} (n \times m) = \begin{bmatrix}
Z
\end{bmatrix}(n \times m) + \begin{bmatrix}
V
\end{bmatrix}(m \times m)$$
![[Pasted image 20251105095520.png]]

If we have this, where `PC = Z * V`. If we try to solve like the following: $$PC = Z *V$$$$PC * V^{-1} = Z * V * V^{-1}$$
$$Z = PC * V^{-1}$$
or more interestingly, $$Z = PC * V^T$$We could say that we are working with PC's, where we are working with less predictors, we can recompute Z within this lesser feature space, which is very useful. 

1) $$R(X) = C(Z) \rightarrow diag(X) = \begin{bmatrix}
\lambda_{1} && 0  \\
0 && \lambda_{2}
\end{bmatrix}$$
2) $$\sum var(R) = \sum var(PC) = \sum^{m}_{j=1} \lambda j = m$$
3) $$\%\text{Explained} \space var(\lambda _{j}) = \frac{\lambda_{j}}{m} = \frac{\lambda_{j}}{\sum \lambda_{j}}$$
**Other Dimensionality Reduction Techniques**
For when we have data that is not linear, we can have a situation like this:
![[Pasted image 20251105101717.png]]
Can we apply some kind of transformation to effectively "unroll" the data? 
This is called *manifold learning*. A manifold is an object in space that appears locally euclidean, but overall is something different. The Earth is manifold, where to us it appears flat, but looking beyond locally, it is a sphere. 
Although the dimensionality is massive, we can still flatten it and keep it an acceptable situation. 

One applicable example: [ml_other_dim_reduction_techniques.ipynb](https://gist.github.com/eitellauria/4321ea2424ca1e7bf7fbedf7e9cc927a)
Using local embedding:
![[Pasted image 20251105102034.png]]
SkLearn has a number of algorithms that can do this for us. 

**TSNE** - one useful algorithm, usually used in visualization. 
"T distributed neighbor embedding "
This algorithm takes a multidimensional dataset and places it in 2D, which is good for visualizing data. Typically, when we have multidimensional dataset with clusters or regions of data, TSNE is good at displaying those clusters cleanly. 

![[Pasted image 20251105102303.png]]

Human beings are really good at pattern recognition in 2D, so having a tool that allows us to do this is very convenient. We can for example use TSNE on the full set of dimensions to see how the data is organized and analyze what it is actually representing. 



