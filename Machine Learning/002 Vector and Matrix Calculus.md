## Scalar Derivatives 

#ScalarDerivativeRules
Instantaneous Rate of Change
![[Pasted image 20250901160921.png]]

**Gradient** the gradient vector is a 2D vector that represents or points toward the direction of the rate of fastest increase. If the gradient of the function is non-zero at a point p, the direction of the gradient is the direction in which the funtion increases most quickly from p, and the magnitude of the gradient is the rate of increase in that direction. 

![[Pasted image 20250901164453.png]]

The gradient plays a fundamental role in **optimization** theory, and therefore in machine learning, where it is used to maximize a function by gradient ascent (or by its inverse, minimize a loss function by gradient descent)

**Gradient Visualization**
![[Pasted image 20250901165354.png]]

[Gradient Visualization Applet](https://www.geogebra.org/m/sWsGNs86)

[Matrix Calculus Calculator](http://www.matrixcalculus.org/matrixCalculus)

## Calculus

**Partial Derivatives**
When taking the derivative of a multivariate function f(x, y), all components which we are NOT taking the derivative with respect to will be treated as constants. In most such cases, they will simply drop to 0. 

![[Pasted image 20250903120007.png]]

**Directional Derivative**
Essentially the gradient of the function.
![[Pasted image 20250903120104.png]]
**Note that we denote the transpose T superscript of the vector when written horizontally just because it is easier to write it as such.

Maximizing the above function:
$$
||M||||\nabla f||\cos \theta
$$
Will involve the condition that:
$$
\cos \theta = 1
$$
Meaning that the vector **u** and the gradient of *f* are parallel. 
This is the maximized rate of change, or the goal of gradient descent/ascent. 

**Taylor Expansion and Approximation**
![[Pasted image 20250903120544.png]]
Allows us to approximate a point on a function in the vicinity of a given point x<sub>0</sub>

This is the Taylor Series Approximation for two variables:
![[Pasted image 20250903120951.png]]

When applied in vector calculus:
![[Pasted image 20250903120710.png]]
This gives us a linear approximation of the vector function *f*
**H** is known as the Hessian matrix:
![[Pasted image 20250903120827.png]]

## Vector Derivatives

Assume we have a vector **x** = [x<sub>1</sub>, x<sub>2</sub>, ... x<sub>m</sub>]
and a vector function **y** = [y<sub>1</sub>(x), y<sub>2</sub>(x), ... y<sub>n</sub>(x)]<sup>T</sup>

We want to compute the derivative of **y** with respect to **x**:
In the more general case of vector / vector, this results in a matrix, but in other cases it can result in a vector or a scalar. 

We will use the *Mixed Layout* ruleset, which treats gradients as column vectors.

![[Pasted image 20250903121458.png]]

See[ MatrixCalculusCalculator](http://www.matrixcalculus.org/).

**Derivative of a dot (inner) product of 2 vectors with respect to one of them:**
The derivative of a dot product wTx  with respect to x is a vector of derivatives 
with respect to the components of x.

Consider:

$$
w = \begin{bmatrix}
w_{1} \\
w_{2} 
\end{bmatrix}

\space

x = \begin{bmatrix}
x_{1} \\
x_{2} \\
\end{bmatrix}
$$
Then:
$$
w^Tx = w_{1}x_{1}  + w_{2}x_{2} = f(x_{1}, x_{2}) = f(x): R^2 \to R
$$
So:
$$
\frac{d(w^Tx)}{dx} = \begin{bmatrix}
\frac{\partial f(x)}{\partial x_{1}} \\
\frac{\partial f(x)}{\partial x_{2}}
\end{bmatrix}
= 
\nabla(w^Tx) = \begin{bmatrix}
w_{1} \\
w_{2}
\end{bmatrix} = x
$$


