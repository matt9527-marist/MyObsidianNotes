Subject:
	age --> young
	prescription --> myope
	astigmatism --> no
	tear_prod_rate --> normal 

$$Score (Class) = P(class) \times P(age=x|class) $$
$$\times P(prescription=x|class) $$
$$\times P(astigmatism=x|class) $$
$$\times P(tear_prod_rate=x|class)$$
Or rather: $$-\log P(Y=C_{k}, X) = -\log( \prod^{4}_{i=1}P(x_{i}|Y=C_{k})-\log P(Y=C_{k}) $$
Where `x1​=age, x2​=prescription, x3​=astigmatism, x4​=tear_prod_rate`
and target `Y = contact_lenses ∈ {none, soft, hard}`

Since this is `argmin`, the minimum loss is for "hard," so the classifier should predict
**hard contact lenses** for the new subject.