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
