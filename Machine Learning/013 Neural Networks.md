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
- 1969: Minsky and Parpert 
	- Show the the Perceptron cannot solve the XOR problem. Recall, there is no way to classify the points given by an XOR function using a single line. 
	- The idea of a universal machine using a perceptron was dropped. 
	- This began an AI Winter, where the development in the field decreased dramatically. 
	- The solution that would come later by connectionists is adding a *hidden layer*. Using the hidden layer, we can produce a neural network that can serve as a universal approximator of any function. 
	- It was not yet figured out how to introduce hidden layers, but the framework of feedforward and then backpropagate was there. 

## Neural Networks 
#NeuralNetwork 
Let us consider the structure of a basic neural network:
(see notes)
**Activation**: When we take a nonlinear transformation, for example, recall the formula introduced in logistic regression: $$g(h) = \frac{1}{1+e^{-h}}$$
The derivative of this function: $$g'(h) = g(h) * (1-g(h))$$
The problem is that this derivative is flat, which means that the gradient used to update the weights will be quite small. This reduces the capacity for learning when we have many inputs. 
A different function that the field has taken a liking to is called the **RE**