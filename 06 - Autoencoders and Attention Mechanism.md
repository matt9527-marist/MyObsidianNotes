**What are Autoencoders?**
![[Pasted image 20260312203303.png]]
"*Autoencoding*" is a data compression algorithm where the compression and deocmpression functions are: 
1) data-specific 
2) Lossy
3) Learned automatically (from examples rather than engineered by a human)
In almost all contexts where an autoencoder is used, the compression and decompression functions are implemented with neural networks. 
![[Pasted image 20260312203437.png]]
We enforce our network repeatedly to reduce the information to a smaller size and then regenerate from the smaller size the original data. 
Somewhat similar idea to pooling, except with pooling, we cannot go back. Pooling is much higher simplification and reduction of size. With autoencoders, we are trying to use deep neural networks to *learn the patterns* of the data such that recreation is not possible. 

1- Autoencoders are data-specific, which means that they will only be able to compress data similar to what they have been trained on. This is different from, say, the MPEG-2 Audio Layer III (MP3) compression algorithm, which only holds assumptions about "sound" in general, but not about specific types of sounds. An autoencoder trained on pictures of faces would do a rather poor job of compressing pictures of trees, because the features it would learn would be face-specific.

2- Autoencoders are lossy, which means that the decompressed outputs will be degraded compared to the original inputs (similar to MP3 or JPEG compression). This differs from lossless arithmetic compression.

3 - Autoencoders are learned automatically from data examples, which is a useful property: it means that it is easy to train specialized instances of the algorithm that will perform well on a specific type of input. It doesn't require any new engineering, just appropriate training data.

**What are autoencoders good for?**
Today two interesting practical applications of autoencoders are  
- data denoising (which we feature later in this post),  
- and dimensionality reduction for data visualization.  
- With appropriate dimensionality and sparsity constraints, autoencoders can learn data projections that are more interesting than PCA or other basic techniques.
![[Pasted image 20260312203811.png]]

![[Pasted image 20260312203824.png]]
- Have a hidden layer that is a size much smaller than inputs and outputs, and we enforce it to approximate the original input. 
- It is trying to learn an approximation to the identity function, so as to output x^ that is similar to x. The identity function seems a particularly trivial function to be trying to learn; but by placing constraints on the network, such as by limiting the number of hidden units, we can discover interesting structure about the data.

**Sequence-to-sequence autoencoder**
• If your inputs are sequences, rather than vectors or 2D images, then  
you may want to use as encoder and decoder a type of model that can  
capture temporal structure, such as a LSTM.  

• To build a LSTM-based autoencoder, first use a LSTM encoder to turn  
your input sequences into a single vector that contains information  
about the entire sequence, then repeat this vector n times (where n is  
the number of timesteps in the output sequence), and run a LSTM  
decoder to turn this constant sequence into the target sequence.

**Steps for Encoding**
*Main Idea*
1) Encode the input sequence into state vectors.  
2) Start with a target sequence of size 1 (just the start-of-sequence character).  
3) Feed the state vectors and 1-char target sequence to the decoder to produce predictions for the next character.  
4) Sample the next character using these predictions (we simply use argmax).  
5) Append the sampled character to the target sequence  
6) Repeat until we generate the end-of-sequence character or we hit the character limit.

![[Pasted image 20260312204006.png]]

**Attention**
![[Pasted image 20260312204018.png]]
Attention is proposed as a solution to the limitation of the Encoder-Decoder model encoding the input  
sequence to one fixed length vector from which to decode each output time step. This issue is believed to be more of a problem when decoding long sequences.