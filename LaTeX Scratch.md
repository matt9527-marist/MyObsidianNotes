---
~
---
$$J = -y\log(\hat{y})-(1-y)\log(1-\hat{y}) + \frac{\lambda}{2}||w||^2$$
$$w^Tx + b$$
$$\hat{y} = \sigma(h) = \frac{1}{1+e^{-h}}$$


$$\frac{d}{dh}\sigma(h) = \sigma(h) * (1-\sigma(h))$$
$$\frac{d(w^Tw)}{dw} = 2w$$

$$h = w^Tx + b$$
$$\hat{y} = \sigma(h))$$
$$J = -y\log(\hat{y})-(1-y)\log(1-\hat{y})$$

$$d\hat{y} = -\frac{y}{\hat{y}} + \frac{1-y}{1-\hat{y}}$$
	$$dh = d\hat{y} * \frac{ \partial \hat{y} }{ \partial h } =  $$