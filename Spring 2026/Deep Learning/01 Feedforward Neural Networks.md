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

**Hidden Layers**
	Obviously, 0 hidden layers results in no change to a reported loss. 
	Starting with only one hidden layer with 2 neurons appears to have the test and training loss level out without fully reaching 0, at least according to the test website. 
	Adding upwards of 3 layers without changing any other parameters results in relatively slow learning, and the test loss drops in time steps. 
	When you add 6 layers, the test error begins to oscillate, which tells us that it is overfitting to the relationships in the training data. That is, if the data is not as complex. 

**# of Neurons**
	Increasing neurons per layer increases training time and accuracy for complex input data. 
	Decreasing neurons reduces training time and computational cost. 

**CNNs**
	Works great for images. Uses feature extraction and classification layers to learn patterns in visual data. 

**Dense Layer**
	Gives the model the ability to explore all the connections between final extracted features. 

**Number of Epochs**
	As we increase number of epochs, we intend that the cost/error score should decrease for the training dataset. However, for the testing (evaluation) dataset, we might expect it to decrease up to a certain point and then start increasing (overfitting)
	Up to that point where the performance stops improving, we need to stop and analyze there. 
	That is the point where learning => memorization.

**# Iterations per Epoch**
	The model processes more batches per epoch. 
	Iterations -> number of overall passes where we update the weights (forward/backward pass)
	Batch Size -> how many training samples out of the whole training dataset do we want to train per iteration? 
	Increasing iterations would mean that we decrease batch size, and vice versa. 
	Increasing iterations would mean that there is more noise/error, but less computational cost. 
	Decreasing iterations would mean there is less noise/error, more computational cost, but less ability to capture complex patterns. 
	Keep in mind that when we use batch learning, we are aggregating these weight updates within the batch. Also, with datasets with more complex patterns, lower iterations cannot work well with regression. 

**Pooling Layers**
	Pooling layers are used when we have CNNs and images.
	We do not want to compute the weights for every single pixel in an image, so we will use a pooling layer (max pooling / average pooling) to expedite the process.
	The processing time we need would be greatly reduced, but it is also possible that we may lose important information. More pooling layers may reduce the accuracy of the network. 

**Normalization Layer**
	We should use the normalization in CNNs or when our data is very varied. 

**Learning Rate**
	High learning rate might slingshot the model or cause it to oscillate around the global minima loss. Low learning rate might slow the model down so much that it may never converge / weights are not updated with enough change. 

**Size of each Image**
	Concerns dimensionality and processing time. 

**Early Stopping**
	Where can we predict the stopping condition where training accuracy increases and validation accuracy diverges? 

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
2) Validation - used to measure the bias of the fitted model to the training dataset. This is to prevent overfitting by avoiding values that match the patterns but fail when dealing with new data. 
3) Test - data unseen by the network used to evaluate the final fitted model. 

**K-Fold Cross Validation**
Shuffle the Dataset Randomly shuffle the dataset to ensure that the data is evenly distributed across all folds.
Split the Dataset into k Folds Divide the dataset into k subsets (folds) of approximately equal size.
Iterate Through Each Fold For each fold: Use the current fold as the test set. Use the remaining k-1 folds as the training set.
Train the Model Train the machine learning model on the training set.
Evaluate the Model Test the model on the test set and record the performance metric (e.g., accuracy, precision, recall).
Repeat for All Folds Repeat steps 3–5 for all k folds, ensuring each fold is used as the test set exactly once.
Calculate the mean and variance of the performance metrics across all folds to estimate the model's generalization ability.

![[Pasted image 20260129201240.png]]
There are several different loss functions that we can select. 
**Probabilistic Loss** - when we do the classification task, we are using probabilities. When there is higher probability for class X, the sample will go to that class. 
**Regression Loss** - for tasks when the target and the sample data is numerical. 

![[Pasted image 20260129201835.png]]
How does **Gradient Descent** work?
Step 1 - randomly initialize weights. 
Step 2 - Loop until convergence: 
	Step 3 - Pick a batch of `B` data points 
	Step 4 - Compute the gradient and what error is responsible for what node. 
		- Eta is the learning rate. If learning rate is too small, it takes too many steps to reach the minimum, and if it is too high, the steps will oscillate. 
	Step 5 - Update the weights. 
		- Attempt to reach the global minimum for error 
Step 6 - Return the weights.

**Epoch, batch size, iteration, and steps per epoch**
![[Pasted image 20260129202627.png]]
• one epoch = one forward pass and one backward pass of all the training examples
- When we see Epoch 1/10, 10 means the number of samples in the batch size. 
• Batch/mini-batch size = the number of training examples in one forward/backward pass. The higher the batch size, the more memory space you'll need.
• number of iterations = number of passes, each pass using [batch size] number of examples. To be clear, one pass = one forward pass + one backward pass (we do not count the forward pass and backward pass as two different passes).
- Number of times the network processes one batch of data. (calculating the loss, propagating the error, updating the weights)
• steps per epoch = Total number of steps (batches of samples) to yield from generator before declaring one epoch finished and starting the next epoch. It should typically be equal to ceil(num_samples / batch_size). Optional for Sequence: if unspecified, will use the len(generator) as a number of steps.

**Batch Size Trade-Off**
![[Pasted image 20260129203246.png]]
Lack of generalizabiliyt => overfitting. We do not prefer to put all the data in one batch. 

**Feature Scaling**
![[Pasted image 20260205192031.png]]
What problem might we face when we have data that is not properly scaled? 
Try to avoid inputs that are not centralized, as it can result in a zig-zag oscillation pattern, where the gradient fails to capture the information well. 

For example, if the data is biased in one direction, when we try to solve it with *gradient descent*, we will face an environment that is biased towards one direction. This takes a lot of time for the model to converge. 
![[Pasted image 20260205192435.png]]

Centralizing the original data is not limited to deep learning algorithms, many machine learning algorithms such as regressions and K-nearest neighbors requires normalization and zero-centralization.

*Can we extend data scaling from the input data to the other layers?*

**Normalization Layers**: 
*Batch Normalization*: An internal covariate shift occurs when there is a change in the input distribution to our network. When the input distribution changes, hidden layers try to learn to adapt to the new distribution. This phenomena can happen after each mini-batch when the weights are updated. This slows down the training process.