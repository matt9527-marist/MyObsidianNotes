Matrix A: $$A = \begin{bmatrix}
a_{11} & a_{12} \\ \\
a_{21} & a_{22} \\
\end{bmatrix}$$
Vector x:
$$x = \begin{bmatrix}
x_{1}  \\
x_{2}
\end{bmatrix}$$
Begin by computing A* w: $$\begin{bmatrix}
a_{11} & a_{12}  \\
a_{21} & a_{22}
\end{bmatrix} * \begin{bmatrix}
x_{1} \\
x_{2}
\end{bmatrix} = \begin{bmatrix}
a_{11}x_{1} + a_{12}x_{2} \\
a_{21}x_{1} + a_{22}x_{2}
\end{bmatrix}$$
Therefore:
$$\frac{d}{dx}(A*x) = \frac{d}{dx}\begin{bmatrix}
a_{11}x_{1} + a_{12}x_{2} \\
a_{21}x_{1} + a_{22}x_{2}
\end{bmatrix}$$
$$= \begin{bmatrix}
\frac{d}{dx_{1}}(a_{11}x_{1} + a_{12}x_{2}) & \frac{d}{dx_{2}}(a_{11}x_{1} + a_{12}x_{2})  \\
\frac{d}{dx_{1}}(a_{21}x_{1} + a_{22}x_{2}) & \frac{d}{dx_{2}}(a_{21}x_{1}+a_{22}x_{2})
\end{bmatrix}$$
$$= \begin{bmatrix}
\frac{d}{dx_{1}}(a_{11}x_{1}) & \frac{d}{dx_{2}}(a_{12}x_{2})  \\
\frac{d}{dx_{1}}(a_{21}x_{1}) & \frac{d}{dx_{2}}(a_{22}x_{2})
\end{bmatrix}$$
$$= \begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix} = A$$
So the derivative of the product of matrix A times a vector x w.r.t. 