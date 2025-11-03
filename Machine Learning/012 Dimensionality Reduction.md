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


