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

**Criteria for Activation Functions**
Nonlinear function  
The composition of linear functions is just another linear function, so you gain nothing by having  
multiple layers; you might as well just do some kind of linear regression or classification.  
Monotonic function  
The activation function should be either entirely non-increasing or non-decreasing. If the  
activation function isn't monotonic then increasing the neuron's weight might cause it to have less 
influence on reducing the error of the cost function.  
Differential  
The activation function should be differential because we want to calculate the change in error  
with respect to given weights at the time of gradient descent.  
Quickly converging  
the activation function should swiftly reach its desired value.  
Zero-centered  
Output of the activation function should be symmetrical at zero so that the gradients do not shift  
to a particular direction.  
Robust to vanishing problem  
The depth of the network and the activation shifting the value to zero.

