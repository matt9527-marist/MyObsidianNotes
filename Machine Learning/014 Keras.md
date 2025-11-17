## Keras 
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
