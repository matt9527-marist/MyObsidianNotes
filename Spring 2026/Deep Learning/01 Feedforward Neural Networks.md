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