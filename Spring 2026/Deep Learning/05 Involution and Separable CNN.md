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
![[Pasted image 20260226191211.png]]

## Involutional Neural Networks 
![[Pasted image 20260226191355.png]]
Not only do we have one kernel to perform analysis. 
- The input is applied to one kernel by itself and then applied to the 3x3 kernel. 
	• The idea is to have an operation that is both *location-*  
	*specific and channel-agnostic*. Trying to implement these  
	specific properties poses a challenge. With a fixed number of  
	involution kernels (for each spatial position) we will not be able  
	to process variable-resolution input tensors.  
	• To solve this problem, the authors have  
	considered generating each kernel conditioned on specific spatial  
	positions. With this method, we should be able to process  
	variable-resolution input tensors with ease. The diagram below  
	provides an intuition on this kernel generation method.
Process tensors within multiple resolutions 
- The CNN assumption is that the pixels that are nearby each other provide some information. Involutional neural networks assume that not only the pixel's neighbors, but also adjacent channels, affect the pixel. Channels can involve color or a variety of aspects like time. 

**Separable Convolutions**
![[Pasted image 20260226191716.png]]
• A Separable Convolution is a process in which a single  
convolution *can be divided into two or more convolutions to*  
*produce the same output*. A single process is divided into two or  
more sub-processes to achieve the same effect. Let’s understand  
Separable Convolutions, their types in-depth with examples.  
• Mainly there are two types of Separable Convolutions  
	• Spatially Separable Convolutions.  
	• Depth-wise Separable Convolutions.

Using these can significantly reduce the computation needed. 
![[Pasted image 20260226191744.png]]
When we want to apply the multiplications, instead of applying a 3x3 kernel to have the next layer, if it is *separable*, I can first apply on a kernel of 3x1, and then we have an outcome that we can apply to a 1x3 kernel. 
- Instead of multiplying 3x3 once, we do two operations of 3x1 and 1x3. 
- Instead of doing 9 multiplications with our input, we are just performing on 6. 
	- Warning: all the kernels are not separable. It should be the case that we have a kernel like above that we can rewrite as the multiplication of column-wise and row-wise matrix. 

![[Pasted image 20260226192045.png]]
