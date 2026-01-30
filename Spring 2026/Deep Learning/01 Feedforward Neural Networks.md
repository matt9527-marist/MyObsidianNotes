![[Pasted image 20260129190822.png]]
Deep Learning Trends:
![[Pasted image 20260129190834.png]]

![[Pasted image 20260129190928.png]]
Through input of data instances in a series of layers, continuously, we can eventually reduce the loss score, representative of error. 
![[Pasted image 20260129191309.png]]
A: Higher level POV
B: Linear representation 
C: Feedforward example 
D: Backpropagation example 

• https://playground.tensorflow.org/  
• https://cloud.google.com/blog/products/ai-machine-learning/understanding-neural-networks-with-tensorflow-playground

In Classification, consider the decision boundary. For any incoming data sample that we make a decision, if the sample falls on the side of class A, it will be classified as that, and if the sample falls on the side of class B, it will be classified as that. This may come with some misclassification with complex data. 
![[Pasted image 20260129191916.png]]
There are several parameters available for tuning. 
One important parameter is number of tunable parameters: 
Obviously, 0 hidden layers results in no change to a reported loss. 
Starting with only one hidden layer with 2 neurons appears to have the test and training loss level out without fully reaching 0, at least according to the test website. 
Adding upwards of 3 layers without changing any other parameters results in relatively slow learning, and the test loss drops in time steps. 
When you add 6 layers, the test error begins to oscillate, which tells us that it is overfitting to the relationships in the training data. 

![[Pasted image 20260129194649.png]]
Mathematical Formulation:
![[Pasted image 20260129194701.png]]

Linear functions are those whose graph is a straight line.  
y = f(x) = a + bx  
![[Pasted image 20260129194739.png]]
Non-linear means the graph is not a straight line. The graph of  
a non-linear function is a curved line. A curved line is a line  
whose direction constantly changes.

**Activation Function**
Linear Activation function: produces a straight line, fails to separate our environment to the two categories if our data is not linearly separable. That is the case most of the time. 
Nonlinear Activation function: Have smarter perceptrons, such that we can detect nonlinear decision boundaries. 

### Common Activation Functions 
![[Pasted image 20260129194929.png]]

**Example of Forward Propagation with Sigmoid**
![[Pasted image 20260129195116.png]]
We can see why Sigmoid works with the shape of its graph. We can see a separation between samples possessing values between -2 and 2 .
TanH and Leaky RELU squeeze the Sigmoid function more, to reduce our area of uncertainty. 

**Strengths and Limitations of a Single Perceptron**
![[Pasted image 20260129195728.png]]
Single perceptron cannot capture XOR for example. 

**Criteria for Activation Functions**
**Nonlinear function**  
The composition of linear functions is just another linear function, so you gain nothing by having  
multiple layers; you might as well just do some kind of linear regression or classification.  
**Monotonic function**  
The activation function should be either entirely non-increasing or non-decreasing. If the  
activation function isn't monotonic then increasing the neuron's weight might cause it to have less 
influence on reducing the error of the cost function.  
**Differential**  
The activation function should be differential because we want to calculate the change in error  
with respect to given weights at the time of gradient descent.  
**Quickly converging**  
the activation function should swiftly reach its desired value.  
**Zero-centered**  
Output of the activation function should be symmetrical at zero so that the gradients do not shift  
to a particular direction.  
**Robust to vanishing problem**  
The depth of the network and the activation shifting the value to zero. 
*Vanishing Problem* - when we propagate error from the last layer, we propagate over all the layers, and the error gradient vanishes by the time it reaches the initial layers. 

**Samples of Monotonic Functions**
![[Pasted image 20260129195802.png]]

![[Pasted image 20260129200058.png]]

Using linear functions, no matter how many layers,  
essentially boils down to the "perceptron" architecture.
**Why do we need nonlinear functions**?
If we have a linear function, it does not matter how many layers we have. The output boundary will always just be a straight line, so we cannot capture a more complex decision boundary. 

**What is the most efficient neural network?**
- *We want a model that demands the LEAST computational time while providing the HIGHEST accuracy*. 
	- We want the smallest number of neurons possible for good accuracy. 
- *Use the least possible perceptron and hidden layers as possible and select the best weights such that the network is the most efficient*
How do we discover this? (How do we select weights for a neural network?)

1) Start with educated guesses / random weights 
2) Evaluate the performance of the NN 
3) Based on optimizer, we update the weights. 
(perform step 3 and 2 repeatedly as long as we have new data and reach the desired performance of the model)
We update the weights using **backpropagation**. There are several alternatives. How do we get the error that allows us to inform the weights on the goal? The **loss function**. 

**The Loss Function**
![[Pasted image 20260129200735.png]]
Identifies the error that we need to reduce. 
How do we *split the data?*
1) Training - what we use to fit the model 
2) Validation - 