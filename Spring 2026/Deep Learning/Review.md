**When might a deeper model generalize worse?**
- When we have a small amount of data, with many layers, we have many parameters. Do we have enough data to justify tuning all of these parameters? Without enough data, we will resort to memorization, rather than generalization. 
- The other condition is when we do not use the proper regularization.
**Why are deeper networks preferred even if a single hidden layer network can approximate any function?**
- Let us use the example of an input image. 
- We want to have a hierarchical learning structure where we want to get from simpler features to more complex features. For instance, in layer 1, we might want to learn about edges, and in layer 2, we learn about corners, layer 3 parts, layer 4 objects, etc. 
- Hierarchical representation 
**Why do neurons "die" in ReLU, suggest fixes**
- Consider the shape of ReLU. If the output of the activation becomes negative, the update becomes 0. Those neurons will "die."
- With Leaky ReLU, we keep movement possible by ensuring that the output will still give an effect. 
**Compare parameters of a 256x256x3 image into (A) a 1000-unit fully-connected layer and (B) a 64 filters of 3x3 convolution**
- For FC, we pass all. This would result a huge number of parameters. 
- For a CNN, this would 3 * 3 * 3 * 64 parameters, 3x3 kernels for 3 channels (RGB), which would result in far fewer parameters. 