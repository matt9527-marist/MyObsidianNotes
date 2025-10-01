## Bayesian Learning Review 
Within Bayesian Learning, we have a joint probability of the data and the target:
`P(x,y) = P(x|y) * P(y)`
This is a way of finding the criterion for classification. The value that maximizes this joint probability. We are taking the joint probability of the data and the target, and whichever class maximizes it is the choice of the model. 
In the framework which we have been working, we need to find a probabilistic architecture by defining a *loss function* that we need to minimize. 
- We use logarithms because it is a monotonic function. We get negative numbers instead of increasingly small multiplied numbers. 
- `logP(x,y) = logP(x|y) * logP(y)`
$$J = -\log P(x,y) = -\log P(x|y)-\log P(y)$$
Coming up with the solution to this loss function requires a lot of data. To make this easier, we can use **Naive Bayes**, and assume that all of the inputs are independent. 
$$P(\vec{x}|y) = \prod^{m}_{j=1}P(x_{j}|y)$$
With this we obtain:
$$J = -\sum^{m}_{j=1}\log P(x_{j}|y)-\log P(y)$$
The next problem we had to consider was **event models**. Do not assume that all of the data will be discretized. 
1) **Categorical Model**: $$P(x_{j}|y_{i}) = \frac{N_{ij} + 1}{N_{i} + k_{j}}$$
   Where we add a 1 at the numerator and the cardinality `k_j` in the denonimator to avoid dealing with a zero frequency. 
2) We saw a variation of the above model when the model corresponds to binary OHE: Bernoulli distribution: **BernoulliNB**: $$P(x_{j}|y_{i}) = \frac{N_{ij} + 1}{N_{i} + 2}$$
3) **Continous (GaussianNB)**: We are to assume that the data is normally distributed. This probability is now a probability density: $$f(x_{j}|y_{i}) = N(\mu_{ij}, \sigma_{ij})$$
   The mean and the standard deviation change for each of the attributes. 
4) **Multinomial**: Refers to a distribution of counts: Imagine the following situation: we have a jar of red, green, and blue marbles, 20 in all. We want to compute the probability of extracting from the jar exactly 2 R, 2 G, and 2 B. Multinomial probabilities predict over counts. 
   Suppose: 8R, 3G, 9B
   The multinomial distribution: $$P(N_{R},N_{G},N_{B}) = \frac{N!}{N_{R}!,N_{G}!,N_{B}!}P_{R}^{N_{R}}*P_{G}^{N_{G}}*P_{B}^{N_{B}}$$
   Notice the factorial operations. This is because we can get many configurations for a given result. We are in a combinatorial situation. 
   In this case, the probabilities are:
   P_R = 8 /20
   P_G = 3 / 20
   P_B = 9 / 20
   And we obtain: $$P(N_{1}\dots N_{k}) = \frac{N!}{\prod^{k}_{j=1}}\prod^{k}_{j=1}P_{j}^{N_{j}}$$

## Text Classification 
Suppose we have *m*, which is a corpus of documents: j_1, j_2, ..., j_m as X
Let's say those texts are the complete works of Shakespeare or something that has a signature that can differentiate the documents from each other. 
We want to infer from the data which document is which (Y).
What problems do we find here?
- We have been working with data that is for the most part of *fixed length*. 
- Documents like books are not fixed length.
One possible approach: 
- Build a **term frequency** matrix:
(see notes)
We can use a dictionary or vocabulary matrix to split the documents according to which words or phrases appear in the text. For example, if we find that the word "news" appears 3 times, it will be listed in the matrix as 3 like shown. 
Of course, this does miss context, but for right now, we are not considering it. This is called a **Bag of Words (BOW)**. We are simply vectorizing the document in terms of as many dimensions as the dictionary has. Therefore, if we have a dictionary full of 400,000 words, we may get a matrix that is quite sparse, with lots of zeroes in the table. We also have to consider the frequency of stop words, like "and" or "there" because they can cause noise to the data, but depending on the purpose of the model, we may want to keep them to preserve meaning or context. 

Keep in mind the categorical model: `P(x|y) = (Nij + 1) / (Ni + kj)`.
What we want to do is compute the probability: `P(d,yi) = P(d|yi) * P(yi)`
where *d* is a given document that we want to predict the class of. How do we compute `P(d|yi)`?

$$P(d|y_{i}) \propto \frac{N!}{\prod^{m}_{t=1}}\prod^{m}_{t=1}P(w_{t}|y_{i})^{N_{t}}$$
Which is the same as the above multinomial probability model. 
Recall that we have been using logarithms for classification: 
$$-\log P(d, y_{i}) = -\log P(d|y_{i}) - \log P(y_{i})$$
And now we need to calculate the probability of a word given the class:
$$P(w_{t}|y_{i}) = \frac{count(w_{t},y_{i}) + 1}{\sum^{ }_{w \in |v|}count(w,y_{i}) + |v|}$$
Where `count(wt,yi)` is the count of the number of words in a given class over the summation of all the words in the dictionary. This is the full expression essentially the same thing as the categorical model's equation. 

Thus we can proceed by using logarithms to simplify the multiplication steps into addition.
$$\min -\log P(d,y_{i}) = -\sum^{m}_{j=1}N^{t}\log P(w_{t}|y_{i}) -\log P(y_{i})$$
This entire expression above can be placed in terms of vectors simply as:
$$-\log P(d,y_{i}) = \vec{t}_{f}^{T}\log \vec{p} + b$$
The summation can be written elegantly as a *vector of term frequencies* times the logarithm of each of the individual probabilities of the words for a given class, plus *b*, which is the bias or the priors of the classes. 


