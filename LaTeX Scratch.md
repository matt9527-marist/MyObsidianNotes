---
~
---
$$\text{Relative Displacement Vector}$$
$$D(t_{i}) = T(t_{i}) - C(t_{i})$$
$$\text{Distance to target } r_{i} = ||D(t_{i})||$$
$$\text{Relative Speed } v_{i} = ||D(t_{i}) - D(t_{i-1})||$$
$$\text{Let } \begin{bmatrix}
t_{a} \implies \text{on target} \\
t_{b} \implies \text{loss of target} \\
t_{c} \implies \text{anomalous speedup} \\
t_{d} \implies \text{correction start}
\end{bmatrix}$$
$$t_{a} < t_{b} < t_{c} < t_{d}$$
$$\text{for frames } t_{i} \leq t_{a}:$$
$$r_{i} \approx 0$$
$$\text{for } t_{a} < t_{i} \leq t_{b}:$$
$$r_{i} > r_{i-1} \implies \frac{dr}{dt} > 0$$
$$\text{for } t_{b} < t_{i} \leq t_{c}:$$
$$\text{1) } r_{i} > r_{i-1} \implies \frac{dr}{dt} > 0$$
$$\text{2) } v_{i} > v_{i-1} \implies \frac{dv}{dt} > 0$$
$$\text{3) } D(t_{i}) * D(t_{i-1}) > 0$$

$$\text{for } t_{c} < t_{i} \leq t_{d}:$$
$$v_{i} < v_{i} - 1 \implies \frac{dv}{dt} < 0$$