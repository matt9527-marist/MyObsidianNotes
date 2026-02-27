![[Pasted image 20260226194950.png]]
Each comes with a host of optimization algorithms to be used to improve performance. 
- MLP the baseline, where we need stochastic gradient descent. 
	- In MLPs, all the perceptrons in one layer are fully connected to the previous one.
- CNN, convolutions and pooling, kernels. 
	- When we want to look at the input from the last layer, we just look at the output from the kernel and the kernel size. 
- RNN: This layer's perceptrons not only get the weights or values from the input, but they also get it from themselves. 

**Recurrent Neural Networks (RNN)**
![[Pasted image 20260226195251.png]]
What is happening in the hidden layer?
- This works based on time. 
- On the first step, we have an input of x.
- For subsequent new inputs, *we take the value from the last iteration/epoch and use it as an input in the next step.*
- The loop that we see in the image is defined according to the time/iteration. We are using that previous output in the next step. 

![[Pasted image 20260226195233.png]]
The implementation can be rather complex in practice. 
- At the top of the image, these are the iterations. How can we formulize this? 
![[Pasted image 20260226195920.png]]
- We have the activation function and outcome `y`. Notice that this is indexed by time `t`. Notice that the activation is the previous weights' output combined with the current iteration and bias. 

**Pros and Cons of Typical RNN**
![[Pasted image 20260226200123.png]]
- Useful whenever we have time series and what to make a prediction. 
- Requires a lot of computation.
- As we update the weights, we will lose the information of past iterations, and we cannot consider future input for the current state. 
**Base RNN Layer**
![[Pasted image 20260226200310.png]]
We have the simple implementation given to us by Keras. 
We also have many hyperparameters to define. 

![[Pasted image 20260226200342.png]]
We have various structures of RNNs to choose from depending on the problem. 
- **one-to-one**: outcome just goes through one element. 
- **one-to-many**: As we can see, one input is given to several outputs. The first element is the number of inputs and the second element is the number of outputs. 
- **many-to-one**: Have several inputs but have one output. Useful for semantic analysis. Take in all of the input through the iterations and then give the output at the end. 
- **Symmetric many-to-many**: Name entity recognition. We pass a sentence to an LLM and then ask for the names, adverbs, adjectives, etc. 
- **Asymmetric many-to-many**: Machine translation, language translation. We know that the structure of a sentence can be different from one language to another, so we cannot go one by one. Get all of the input, absorb the concept, and then generate the outcome. 

![[Pasted image 20260226200802.png]]
How do we define our loss function in RNNs? 
- The output is dependent on the time, so our loss function is also dependent on the time. 
How do we define our backpropagation? 
- This is the same derivative, but with the difference that now, when we want to compute the chain of derivatives, we do it based on the weights. 

**Deep RNN**
![[Pasted image 20260226200924.png]]
In theory, an RNN can remember the entire stream of input values. However, gradient magnitude tends to decay as you move backwards from the loss signal. So earlier inputs may not contributed much to the RNN's final answer at the end. For a transducer, inputs may contribute little to the output for locations some distance away. This phenomena is called *vanishing problem*. "gated" versions of RNNs can handle this problem. These RNNs include separate vectors (the "gates") which control which parts of the unit's state will be updated at each timestep.
- These gates will control how much we want to remember from the past. 

![[Pasted image 20260226201248.png]]
Based on these elements, we will end up with two types of gated RNNs:
1) GRU: Gated Recurrent Unit 
2) LSTM: Long Short-Term Memory 
![[Pasted image 20260226201437.png]]
