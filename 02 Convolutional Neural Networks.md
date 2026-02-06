We have started with standard MLPs: 
![[Pasted image 20260205194304.png]]
A neural network can function alright with providing a classification for a centralized input image. The way that this works, the MLP takes the input row by row of pixels. 
- When the input is NOT centralized, the input will be of a completely different shape that is not recognized. 

**Translation Invariance provide by CNN**
![[Pasted image 20260205194345.png]]
CNNs use a sliding window to search for elements (pixels) within an image to find a given pattern. 
- Convert an image (32x32x3) to a cube.
- Separating the image into tiles, if the desired pattern is found anywhere among those tiles, the model should be able to recognize that. 

> A convolutional layer is defined by the filter (or kernel) size, the number of filters applied and the stride.

![[Pasted image 20260205194805.png]]![[Pasted image 20260205194853.png]]

**Batch Normalization**
- Why use batch normalization? 
	- The distribution of the output can greatly affect how the model makes its decisions. 
	- Consider a leftmost-skewed distribution for the Sigmoid function, the function will determine the data as being mostly near 0. 
![[Pasted image 20260205195029.png]]

**Training Computational Complexity of DNNs**
The complexity of a DNN is dependent on the following factors:
- The number of neurons / perceptrons. 
- The general rule is that MLP < CNN in terms of computation complexity and cost. 
- CNNs suffer from too many trainable parameters, impacting computational performance 

![[Pasted image 20260205195341.png]]

The first layer of LeNet has 784 neurons as an input. This is huge. 
However, consider what happens when we pass it to the convolutional layer with a 5x5 kernel and 2 (28x28x6) padding (the portion where the kernel reaches the edge of an image where it is too large and needs to cover empty pixels). The number of neurons in that layer will increase to 4704!
- To control the number of neurons, we shift between the convolutional and pooling layers. 
- Some solutions: 
	- *Input Size Reduction* - simply decrease the resolution of the image. 
	- Feature reduction/selection - average/max pooling: keep/take only the most important features i 
	- 