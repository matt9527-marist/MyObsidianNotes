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
A different function that the field has taken a liking to is called the **RELU Activation Function**. 
(see notes)
For any hidden layer in MLPs, RELU is the standard. Depending on the nature of the problem, of course. We may want to use sigmoid instead for something like binary classification. If it is a multi-class classification, we can use softmax. 
In the hidden layers, however, we need some function to *ensure that gradients continue to backpropagate*. 

![[Pasted image 20251110164208.png]]
![[Pasted image 20251110164714.png]]

In summary:
![[Pasted image 20251110165520.png]]
We write all of these computations in vectorized form because modern GPUs can handle the transformations via SIMD.

## Training Neural Networks Using Backpropagation 
#Backpropagation 
• Training is the process of setting the best
weights on the edges connecting all the units in
the network
• The goal is to use the training set to calculate
weights where the output of the network is as
close to the desired output as possible for as
many of the examples in the training set as
possible

![[Pasted image 20251110170012.png]]

Backpropagation is the same as the *chain rule*. 
The mathematics for this is from Calculus. In the multivariate world, it is very similar. 
(see notes)
Whenever we have concurring branches we will have the equation: $$\frac{dZ}{dt} = \sum^{}_{}\frac{\partial Z}{\partial x_{j}} * \frac{dx_{j}}{dt}$$
Doing the computations is particularly cumbersome. This is where the field of *automatic differentiation* comes from. This sows the manner in which we do the computations so that we can move forward. 
When we are computing the derivative of J, or the terminal function, with respect to any parameter, we use the notation: $$\frac{dJ}{d\phi} = d\phi$$
Cleaner than repeatedly writing derivatives (see Andrew Ng. @ Stanford)

Examples:
Logistic Regression (vectorized one observation)
![[Pasted image 20251110175218.png]]

The basic structure for an MLP is an input layer (X), followed by a hidden layer (h), and an output layer (y):
![[Pasted image 20251110175846.png]]
![[Pasted image 20251110175855.png]]
This is the computation for one observation that is passing through and being backpropagated. This is to give us an idea of how complicated things can become. 

These derivations are computed in iterations using Keras and TensorFlow modules via Colab. 
*JAX* is a secondary platform that has seen more recent use. This is more like NumPy. 

Computational graphs of feed forward and back propagate using JAX:
[ml_computational_graphs_in_jax.ipynb](https://gist.github.com/eitellauria/83dd7484f4ac7a3b11d088a4797942de)

[ml_mlp_backpropagation_from_scratch.ipynb](https://gist.github.com/eitellauria/e03f467c136fd7d967f1945feb2316a0)

## Keras and TensorFlow 
![[Pasted image 20251112094300.png]]

**First Look at Keras using MNIST Dataset**
[ml_a-first-look-at-keras.ipynb](https://gist.github.com/eitellauria/ab6dcb4e9d90796b5bbe7c6b3f401a7d)
Also see: [Keras](keras.io), originally only under *TensorFlow*, but now can serve independently. 

Steps to use Keras: 
1) Load data and perform preprocessing 
	- We are discussing multi-dimensional arrays (tensors)
	- Split between train and test data
2) Set up the network architecture: 
```Python
import keras
model = keras.Sequential([
    keras.layers.Dense(512, activation="relu"),
    keras.layers.Dense(10, activation="softmax")
])
```
- Sequential denotes a traditional (garden variety) MLP, or layer by layer 
- The sequential node will have 512 nodes in the hidden layer and 10 output nodes, corresponding to the 10 handwritten digits in the MNIST dataset. 
- No need to specify the input layer in this example. 
3) Compilation step 
```python 
model.compile(optimizer="rmsprop",
              loss="sparse_categorical_crossentropy",
              metrics=["accuracy"])
```
- There are other optimizers that allow us to ensure that we do not fall inside of local minima. 
- We use the original categorical crossentropy, but a sparse version. Sparse is for exposing a number of possible categories as opposed to using one-hot encoding. 
- This is not *fitting* the model, just building the model. 
4) Fit the model 
```python 
model.fit(train_images, train_labels, epochs=5, batch_size=128)
```
- Using the same function provided by SkLearn. 
5) Evaluate predictions 
```Python
test_digits = test_images[0:10]
predictions = model.predict(test_digits)
predictions[0]
```
- We can use the same SkLearn functions to evaluate the accuracy of the predictions. Same was as before. 

**Regression Example**
[ML_Keras_for_regression.ipynb](https://gist.github.com/eitellauria/5434238e6d340baa14e29761d20ac0bf)


