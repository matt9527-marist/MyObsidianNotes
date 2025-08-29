Matrix Operations Examples:

*Matrix Addition*
$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
+
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
=
\begin{bmatrix}
6 & 8 \\
10 & 12
\end{bmatrix}
$$

*Matrix Multiplication*
$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\cdot
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
=
\begin{bmatrix}
1(5)+2(7) & 1(6)+2(8) \\
3(5)+4(7) & 3(6)+4(8)
\end{bmatrix}
=
\begin{bmatrix}
19 & 22 \\
43 & 50
\end{bmatrix}
$$

*Matrix Transpose*

$$
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}^T
=
\begin{bmatrix}
1 & 4 \\
2 & 5 \\
3 & 6
\end{bmatrix}
$$

*Matrix Determinant*
$$
\det\!\left(
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}\right)
= 1 \cdot 4 - 2 \cdot 3 = -2
$$

*Matrix Inverse*
$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}^{-1}
=
\frac{1}{-2}
\begin{bmatrix}
4 & -2 \\
-3 & 1
\end{bmatrix}
=
\begin{bmatrix}
-2 & 1 \\
1.5 & -0.5
\end{bmatrix}
$$

*Eigenvalues and Eigenvectors*

$$
% Eigenvalue problem
A v = \lambda v

% Example
\begin{bmatrix}
2 & 1 \\
1 & 2
\end{bmatrix}
\begin{bmatrix}
1 \\
1
\end{bmatrix}
=
3 \begin{bmatrix}
1 \\
1
\end{bmatrix}

% So eigenvalue \lambda = 3, eigenvector v = [1,1]^T
$$
*Projection*
$$
% Projection matrix onto column space of A
P = A (A^T A)^{-1} A^T

% Example: projecting y onto span of A
A =
\begin{bmatrix}
1 \\
1
\end{bmatrix},
\quad
y =
\begin{bmatrix}
2 \\
3
\end{bmatrix}

\hat{y} = P y =
\begin{bmatrix}
2.5 \\
2.5
\end{bmatrix}

$$
