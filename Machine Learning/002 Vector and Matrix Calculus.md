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

