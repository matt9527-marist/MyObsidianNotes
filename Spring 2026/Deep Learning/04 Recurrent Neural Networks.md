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
- For subsequent new inputs, we take the value from the la

![[Pasted image 20260226195233.png]]
