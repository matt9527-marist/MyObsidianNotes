Problem 4. Given the following vectors:

$$

x = \begin{bmatrix}

x_{1} \\

x_{2}

\end{bmatrix},

a = \begin{bmatrix}

a_{1} \\

s_{2} \\

\end{bmatrix},

b = \begin{bmatrix}

b_{1} \\

b_{2} \\

\end{bmatrix}

$$

Prove that:

$$

\nabla [(a^Tx)\bullet(b^Tx)] = (a^Tx)\bullet b + (b^Tx)\bullet a

$$

The dot operator denotes a regular product (e.g. 2 dot 2=4)


1) Expand the left side:
$$(a^Tx)(b^Tx) = (a_{1}x_{1}+a_{2}x_{2})(b_{1}x_{1}+b_{2}x_{2})$$
$$= a_{1}b_{1}x_{1}^2 + a_{1}x_{1}b_{2}x_{2} + a_{2}x_{2}b_{1}x_{1} + a_{2}b_{2}x_{2}^2$$
$$= a_{1}b_{1}x_{1}^2 + (a_{1}b_{2} + a_{2}b_{1})x_{1}x_{2} + a_{2}b_{2}x_{2}^2$$
2) Take the partial derivative of the left side w.r.t. x1

$$\frac{\partial a_{1}b_{1}x_{1}^2 + (a_{1}b_{2} + a_{2}b_{1})x_{1}x_{2} + a_{2}b_{2}x_{2}^2}{\partial x_{1}} = 2a_{1}b_{1}x_{1} + (a_{1}b_{2}+a_{2}b_{1})x_{2}$$
Simplify:
$$= a_{1}b_{1}x_{1} + a_{1}b_{1}x_{1} +a_{1}b_{2}x_{2} + a_{2}b_{1}x_{2}$$
$$= b_{1}(a_{1}x_{1}+a_{2}x_{2}) + a_{1}(b_{1}x_{1}+b_{2}x_{2})$$
Therefore:
$$\frac{\partial [(a^Tx)(b^Tx)]}{\partial x_{1}} = (a^Tx)b_{1} + (b^Tx)a_{1}$$
3) Do the same as step 2 but w.r.t. x2
$$\frac{\partial a_{1}b_{1}x_{1}^2 + (a_{1}b_{2} + a_{2}b_{1})x_{1}x_{2} + a_{2}b_{2}x_{2}^2}{\partial x_{2}} = 2a_{2}b_{2}x_{2} + (a_{1}b_{2}+a_{2}b_{1})x_{1}$$
Simplify:
$$a_{2}b_{2}x_{2} + a_{2}b_{2}x_{2} + a_{1}b_{2}x_{1} + a_{2}b_{1}x_{1}$$
$$ = b_{2}(a_{1}x_{1}+a_{2}x_{2}) + a_{2}(b_{1}x_{1}+b_{2}x_{2})$$
Therefore:
$$\frac{\partial [(a^Tx)(b^Tx)]}{\partial x_{1}} = (a^Tx)b_{2} + (b^Tx)a_{2}$$
4) When combined into gradient vector:
$$\nabla [(a^Tx)(b^Tx)] = \begin{bmatrix}
\frac{\partial[(a^Tx)(b^Tx)]}{\partial x_{1}} \\
\frac{\partial[(a^Tx)(b^Tx)]}{\partial x_{2}}
\end{bmatrix}=

$$