## Keras
#Keras
Multiple factors to consider when building neural networks, multiple hyperparameters:
– Data Preparation: Scale/ encode inputs and outputs  
– Topology (# hidden layers, # neuron per hidden layer)  
– Hidden layer(s) activation (typically ReLU, may be tanh, avoid  
sigmoid)  
– Output Activation: sigmoid, softmax, linear (for regression)  
– Optimizers (type of gradient descent algorithm)  
– Learning Rate  
– Momentum (more energy to go uphill)  
– Regularization and Dropout  
– How much training? Watch out for overfitting  
– Training, validation and Testing

**Input Scaling / Encoding**
Usually done for better performance.
- Normalize the data before training the model 
- Min-Max, One-Hot-Encoding 

**Hidden Layer Activation Functions**
![[Pasted image 20251117160120.png]]
![[Pasted image 20251117160138.png]]
Do not use *Sigmoid* for anything beyond shallow models, as it will lead to expontentially decreasing gradients (vanishing gradient or gradient saturation), reducing the effectiveness of the training of the model. 

![[Pasted image 20251117160458.png]]
Tends to have the best performance, but comes with the issue of not being able to compute the derivative at the point x = 0. 
We also may want to add a small margin or slope to the function where x < 0 to improve the model's training performance, as shown:
![[Pasted image 20251117160646.png]]

*What about Output Activation?*
Not different from regression, binary classification, or multi-class classification:
- Regression: No activation, it is a linear output. Sum of the weights * activated layers + bias to give us a numerical prediction, which can be a scalar or vector value. 
- Binary Classification: Works with regular Sigmoid activation 
- Multi-class Classification: Works with Softmax. 

**Network Topology**
How do we determine # of hidden layers? # neurons per hidden layer? 
There is no single "best" configuration; it is determined via experimentation. 
Keras has its own tuner, similar to the ones we have been using to do hyperparameter optimization (GridSearch, RandomSearch, Bayesian Search)

**Epochs, Batches, and Steps**
Epoch actually represents a full forward and backward pass, in which the full dataset has been seen:
$$\text{steps per epoch} = \frac{\text{number of training samples}}{\text{batch size}}$$
This is different from the number of steps. 
For every time that we want to update the weights, if we want to go over the entire dataset, it will take a long time to learn. Recall: SGD. We create minibatches of the data instead. 

*Steps* - refers to the batch size. Modern platforms randomize the minibatches so that each epoch does not use the same amount of steps. 
![[Pasted image 20251117162158.png]]
1875 steps over 10 epochs, meaning the model saw the entire dataset 10 times.
This means that we have seen 18750 total updates (steps)

**Optimizers** - Some version gradient descent that we have seen from the beginning. 
	**Momentum** - Give more "energy" to the algorithm so that it can move out of local minima. 
	Like pushing a ball hard enough to move out of a pit. 
	**Adagrad** - Try to direct how the gradient is going to move. The pure gradient's direction is to that of steepest descent. Adagrad modifies the gradient to be the "adaptive gradient." 
	![[Pasted image 20251117163639.png]]
	Adapt the learning rate in the manner that it depends on the squares of the gradients. If certain features are not used frequently (for example in text), perhaps it will give more direction for weights corresponding to those features. The problem is that the squared value never decreases, so it cannot intuitively become smaller. With every pass, the algorithm will become slower. 
	**RMSProp** - Root Mean Squared Propagation 
	![[Pasted image 20251117163933.png]]
	Weighted running average. This looks similar to Adagrad, but it speeds up the process by comparing the average weights to the weight of the previous observations. 
	s_t = weight on old avg. + weight on new observation.
	**Adam** - Controlled in the same manner by a weighted running average. Adaptive in terms of how the gradient is going to move. 
	![[Pasted image 20251117164243.png]]
		Helps us avoid local minima. Momentum gives direction -> faster smoother movement, RMSProp adapts learning rate per parameter -> prevents overshooting, Adam = Momentum + RMSProp

**Early Stopping and Dropout**
*Overfitting and Generalization*
- Generalize from training examples to all possible inputs. 
- We do not want to undertrain, but overtraining is just as bad. 
	- One solution is #regularization. Shrink the parameters via a penalty term, and that way, we can ensure that we do not overfit. (L1 and L2)
	- Suggested by Hinton in 2012: 
		- Use **Dropout**: Wipe out at random some units and their connections from the network via a dropout layer during training. 
	- Another solution is **Early Stopping**
	  ![[Pasted image 20251117165956.png]]
	  Stop on the epochs. Monitor online the value of the loss on the training data and the validation data. When the two values begin to diverge, we stop early. Keep in mind that this illustration is in a perfect world. There is a parameter called `patience`, that allows us to check 2 or more epochs after that divergence point to see if it is indeed a sweet spot to stop. 

**Learning Rate Scheduling**
• Small Learning Rate  
	– With small learning rate, weight adjustments small  
	– Network takes unacceptable time converging to solution  
• Large Learning Rate  
	– Suppose algorithm close to optimal solution  
	– With large learning rate, network likely to “overshoot” optimal  
	solution  

Scheduling - learning rate of an optimizer is adjusted during the training process. 

*Inverse Time Delay* (Power Scheduling):
`learning rate = initial_learning_rate / (1 + step / decay_steps)`
*Exponential Rate Scheduling*: 
`learning rate = initial_learning_rate * decay_rate^(step / decay steps)`
*Piecewise Constant Scheduling*: - divides the training process into intervals:
![[Pasted image 20251117173512.png]]

**Batch Normalization**
