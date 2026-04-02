*Review the Following*:
![[Pasted image 20260312204430.png]]
- With supervised learning, we have a labeled data, and we can always evaluate our model.
- Unsupervised learning is unlabeled, and we have to search for the underlying main idea. 

**Generative Modeling**
![[Pasted image 20260312204628.png]]
We want to create a fake image, video, or text that looks real. How can we tell?
- It should follow the distribution of real data.
- We must find the distribution and find the valid sample that fits the distribution as closely as possible (nearest to reality)

**Why Generative Models?**
![[Pasted image 20260312204649.png]]
Why do we want to create fake data? 
- Remember, this data is difficult for us to distinguish as fake from real. 
- We can use this as synthetic data to help in finding the underlying patterns in the real data. 

**Outlier Detection**
Both advantage and disadvantage. 
If through the generative models, we could learn about the "usual" distributions, they can help us catch the examples that are unusual or unpredictable. 
GANs have the advantage of being able to run tests with these edge cases, but there is still not enough data to process what to do with the edge case. 
![[Pasted image 20260312204808.png]]
The disadvantage is that it is difficult for a model to determine what is real or fake (think the danger of self-driving calls)

**Latent Variable Models**
We want to extend what we have in autoencoders. 
![[Pasted image 20260312204903.png|602]]
What's the main difference between an autoencoder anda

**What is a Latent Variable?**
*Latent variables mean that we do not see the actual result, but based on the effect, we should still be able to infer what is going on*
- We want to learn from examples the actual distributions. The actual distributions we cannot actually see, but we can see their "shadows" or their effects/structure. 
- Autoencoding is the unsupervised approach for learning a lower-dimensional feature representation for unlabeled training data. 
![[Pasted image 20260312205117.png]]
![[Pasted image 20260312205125.png]]
- We have the input, and we can try to reconstruct it to get the output. 
- We compare the input vs. output to obtain the loss function. 
- The loss function does not use any labels, but we want to minimize this as much as possible to enable the model to absorb all of the features.
The only *bottleneck* is the size of the latent space: 
![[Pasted image 20260312205322.png]]
![[Pasted image 20260312205333.png]]

**Where are we?**
![[Pasted image 20260312205401.png]]
Here, we have a normal autoencoder that is learning the input, but not the distribution. We want to learn the distribution so that it can be capable of generation. 
**Variational Autoencoders (VAE)**
![[Pasted image 20260312205426.png]]
Variational encoders sample from the mean and standard deviation to learn the parameters of the input. Now, our formula is changed:
![[Pasted image 20260312205626.png]]

**Reconstruction Loss**
This is simply measured by the log likelihood between input and output. 

**Regularization Term**
![[Pasted image 20260312205748.png]]

**Priors on the Latent Distribution**
![[Pasted image 20260312205758.png]]Why? We want to make sure that we follow the regularization. 
![[Pasted image 20260312205853.png]]

![[Pasted image 20260312210106.png]]
