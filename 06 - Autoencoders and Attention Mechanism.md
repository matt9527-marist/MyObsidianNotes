**What are Autoencoders?**
![[Pasted image 20260312203303.png]]
"*Autoencoding*" is a data compression algorithm where the compression and deocmpression functions are: 
1) data-specific 
2) Lossy
3) Learned automatically (from examples rather than engineered by a human)
In almost all contexts where an autoencoder is used, the compression and decompression functions are implemented with neural networks. 
![[Pasted image 20260312203437.png]]
We enforce our network repeatedly to reduce the information to a smaller size and then regenerate from the smaller size the original data. 

1- Autoencoders are data-specific, which means that they will only be able to compress data similar to what they have been trained on. This is different from, say, the MPEG-2 Audio Layer III (MP3) compression algorithm, which only holds assumptions about "sound" in general, but not about specific types of sounds. An autoencoder trained on pictures of faces would do a rather poor job of compressing pictures of trees, because the features it would learn would be face-specific.

2- Autoencoders are lossy, which means that the decompressed outputs will be degraded compared to the original inputs (similar to MP3 or JPEG compression). This differs from lossless arithmetic compression.

3 - Autoencoders are learned automatically from data examples, which is a useful property: it means that it is easy to train specialized instances of the algorithm that will perform well on a specific type of input. It doesn't require any new engineering, just appropriate training data.
