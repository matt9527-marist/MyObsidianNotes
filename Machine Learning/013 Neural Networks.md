This is the *connectionist* tribe of machine learning, which includes the modern LLMs like GenAI (ChatGPT, Claude, Gemini). This is the main technique focused on modern research. 

The simplest form of a neural network is what we saw with linear regression where, we take a set of inputs `x1...xn` connected via weights to derive an output `yhat`. 
Recall the formulae: $$w^Tx + b = \hat{y}$$
$$L = \frac{1}{2}(\hat{y}-y)^2$$
From a historical perspective, the field of connectionism looks a the functions of the brain and tries to approximate them, by mimicking the design of neurons. 
![[Pasted image 20251110160018.png]]

We our most basic model of a neural network:
(see notes)
The problem with this is that there was no real concept of learning originally. This was 1941, where a number of developments occurred in between then and the 1980s. 
- 1958-1962: The **Perceptron**. (Rosenblatt)
	- Looks similar to a linear regression, but in reality is a different field. 
	- Model itself looks the same where the summation of inputs map to a given step function, but the perceptron enables the ability to learn. 
	- (see notes)
	- This was originally built in software and was tested to try and classify letters. 