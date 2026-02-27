**1D,  2D, and 3D CNNs**
![[Pasted image 20260226184644.png]]
(1-dimensional CNN)
- When we say "1D" recall arrays, matrices, and tensors. 
	- Input is our feature vector
	- Outcome is the feature mapping
- Consider that the input is 12 elements, and output is 12 elements.
- Consider our filter/weights as 1x1, or one pixel. Let's have this filter be multiplication by a value, so the input element gets multipled by the filter value to obtain the output. 

![[Pasted image 20260226185420.png]]
(1-dimensional CNN with 2x1 filter)
- Consider now when we have a 2x1 filter. 
- This filter sums the multiplication of, in this case, (9x3) + (6x7) for the first cell, and subsequent cells follow. 

![[Pasted image 20260226185538.png]]
(1-dimensional CNN with 3x1 filter)
- Notice how there is extra space on the output with this example. 
- We need to do padding to fix this. 
	- Why? Sometimes, our input size is not equivalent to the output that we want. For example, if we work with a dataset of images, we might have pictures of different sizes, but we designed the DNN to always have a specific size of input. 

![[Pasted image 20260226185801.png]]
(1-D CNN 1x3 filter with padding)

![[Pasted image 20260226190113.png]]
(1-D CNN with shifting)
Formula: (W-F+2P) / S + 1

![[Pasted image 20260226190242.png]]
(2-D CNN)
- Works the same way, except this time we have a 2x2 kernel. 
- This mechanism is a good choice for decreasing the size of our input (space invariance) and decreasing the size of the network with which we are working. 
- Our outcome still is decreased. 

![[Pasted image 20260226190422.png]]
(2-D CNN with Padding)

**2-D CNN in practice**
![[Pasted image 20260226190552.png]]
- This is the general structure of convolutional layers followed by pooling layers.
- We can see that the size of the featues continuously go down.

![[Pasted image 20260226191033.png]]
(CNN with depth)
- Consider the depth extending the CNN by colors (RGB)

**N-layer CNN**
![[Pasted image 20260226191103.png]]
As you increase the number of convolutional layers and kernels, we will continuously obtain a smaller output. 