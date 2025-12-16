---
~
---
$$t_{0}, t_{1}, t_{2} \dots, t_{N}$$

$$C(t_{i}) = (x_{c}(t_{i}), y_{c}(t_{i}))$$
$$T(t_{i}) = (x_{t}(t_{i}), y_{t}(t_{i}))$$
$$D(t_{i}​)=T(t_{i})−C(t_{i}​)$$

$$D(t_{i}) = (dx_{i}, dy_{i}) $$
$$D(t_{i-1}) = (dx_{i-1}, dy_{i-1})$$
$$\Delta D(t_{i}) = D(t_{i}) - D(t_{i-1}) = \begin{bmatrix}
dx_{i} - dx_{i-1}  \\
dy_{i} - dy_{i-1}
\end{bmatrix}$$
$$v(t_{i}) = ||\Delta D(t_{i})|| = \sqrt{ (dx_{i} - dx_{i-1})^2 + (dy_{i} - dy_{i-1})^2 }$$
$$D(t)=T(t)−C(t)$$
$$\Delta D(t) = \Delta T(t) - \Delta C(t)$$
$$\Delta C(t) = \Delta T(t) - \Delta D(t)$$