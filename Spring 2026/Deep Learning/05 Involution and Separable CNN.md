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
- This filter s

![[Pasted image 20260226185538.png]]
(1-dimensional CNN with 3x1 filter)
- Notice how there is extra space on the output with this example. 
- We need to do padding to fix this. 
	- Why? Sometimes, our input size is not equivalent to the output that we want. For example, if we work with a dataset of images, we might have pictures of different sizes, but we designed the DNN to always have a specific size of input. 

![[Pasted image 20260226185801.png]]
(1-D CNN 1x3 filter with padding)
