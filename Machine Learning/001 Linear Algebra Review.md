**Vectors** are mathematical objects that have magnitude and direction. 
![[Pasted image 20250827121644.png]]

![[Pasted image 20250827121655.png]]

There is also the **outer product** of vectors, where we take two vectors v<sub>0</sub> and v<sub>1</sub>, which both have dimensions n and m respectively, and we yield an n x m matrix. 

![[Pasted image 20250827122431.png]]

Additional useful material about the vector **norm**:

![[Pasted image 20250827121709.png]]

**Similar Equation for a plane**
In 3D space, we can use vectors in the same way. ![[Pasted image 20250827122029.png]]
As an additional application of a dot product. 

![[Pasted image 20250827121753.png]]

---

![[Pasted image 20250827121825.png]]
![[Pasted image 20250827121850.png]]

**Rank** is involved in dimensionality reduction (PCA). Models can suffer from redundancy in features, which can mean the wasting of resources for computation. 

These relations are also present in Backpropagation.

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


