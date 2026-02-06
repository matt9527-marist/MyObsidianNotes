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
![[Pasted image 20260205194805.png]]

