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
What's the main difference between an autoencoder and a GAN?
*Autoencoder*: Compress input, then reconstruct it. [x --> z --> x], minimizing the difference between the original input and the reconstructed input. 
*GAN*: Generate new samples from the distribution [z --> G(z)], maximizing how real or true the new samples appear. 

**What is a Latent Variable?**
*Latent variables mean that we do not see the actual result, but based on the effect, we should still be able to infer what is going on*
- We want to learn from examples the actual distributions. The actual distributions we cannot actually see, but we can see their "shadows" or their effects/structure. 
- Autoencoding is the unsupervised approach for learning a lower-dimensional feature representation for unlabeled training data. 
![[Pasted image 20260312205117.png]]
![[Pasted image 20260312205125.png]]
- We have the input, and we can try to reconstruct it to get the output. 
- We compare the input vs. output to obtain the loss function, which is the *difference between the input and reconstruction*. 
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
**Difference between Normal Autoencoder and VAE**
A normal autoencoder learns a single compressed input, while a VAE learns a probability distribution over the latent space 
Instead of outputting a single `z`, the encoder outputs the mean and standard deviation to define the distribution, so each input maps to a region in latent space, not single point. 

The following are optimizations we can perform with a VAE:

**Reconstruction Loss**
This is simply measured by the log likelihood between input and output. 

**Regularization Term**
![[Pasted image 20260312205748.png]]

**Priors on the Latent Distribution**
![[Pasted image 20260312205758.png]]
VAEs force the latent variables `z` to follow a normal Gaussian distribution instead of placing points anywhere. 
Encourages encodings to distribute evenly around the center, learning an overall pattern instead of memorizing isolated points of data.

Why? We want to make sure that we follow the regularization. 
![[Pasted image 20260312205853.png|608]]
![[Pasted image 20260402192912.png|609]]
![[Pasted image 20260402192933.png|611]]
![[Pasted image 20260402193017.png|609]]

**VAE Computation Graph**
![[Pasted image 20260312210106.png]]
Cannot do backpropagation because random sampling breaks the gradient flow needed for backpropagation. It needs to be deterministic. 
Because of the sampling function being stochastic (random), `z` is not a smooth differentiable function of the encoder parameters, and as such, we cannot compute the derivative of the loss w.r.t. the encoder parameters. 

**Reparameterizing the Sampling Layer**
Consider the sampled latent vector `z` as a sum of:
- a fixed mean vector
- and a fixed standard deviation vector, scaled by random constants drawn from the prior distribution. 
![[Pasted image 20260402193214.png]]
We want to backpropagate the error. 
(Determinstic => the value stays the same)
We can backpropagate the error using the chain of derivatives when `z` is deterministic. 

**Latent Perturbation**
Slowly increase or decrease the a *single latent variable*, and keep all other variables fixed. 
Different dimensions of `z` encodes different interpretable latent features. 
![[Pasted image 20260402193454.png]]
**Disentanglement**
Ideally, we want latent variables that are uncorrelated with each other. 
Enforce diagonal prior on the latent variables to encourage independence
![[Pasted image 20260402193551.png]]

**Latent Disentanglement with B-VAEs**
![[Pasted image 20260402193620.png]]

**What if we just want to sample?**
![[Pasted image 20260402193939.png|697]]

## Generative Adversarial Networks (**GANs**)
We will generate samples, but it will fight with itself. 
![[Pasted image 20260402194053.png]]
the *generator* (originally the decoding component of the autoencoder) uses `z` to create an imitation of the data to try and trick the *discriminator*, which tries to identify real data from false data created by the generator. The goal is to have the generator create samples that are as real as possile to address the issue of completeness. 
- GANs should force the generator to create fakes as accurately as possible to the reality. 
- The discriminator should also become better and better at separating the fakes from reality. 

**Intuition behind GANs**
![[Pasted image 20260402194342.png|463]]
![[Pasted image 20260402194350.png|462]]
![[Pasted image 20260402194430.png|464]]
![[Pasted image 20260402194454.png|465]]

**Training GANs**
![[Pasted image 20260402194548.png]]
What is our **loss function?** for GANs?
![[Pasted image 20260402194632.png|421]]
Why is this written in this way? 
- Consider the log function. 
- The goal is not to detect the reality, but to detect that the data `D(G(z))` is fake.
- The job is the prediction of the fake, not the prediction of the real. 

![[Pasted image 20260402195253.png]]
**Loss function**: Minimize `D`, Maximize `G`.
This is why the objectives are adversarial. 

**GANs are Distribution Transformers**
![[Pasted image 20260402195356.png]]
We want to transform the way that a specific element is represented, converting what we have learned to what would be the same behavior. 

How can we extend what we have to different objects?

**Conditional GAN(s)**
![[Pasted image 20260402195523.png|505]]
How much data from the fake should be the same as the real data it is being compared to?
CGANs example in pictures:
![[Pasted image 20260402195550.png|506]]

**Review**
*Why does the generator need the discriminator?*
We have a scope/noise, and from it, we generate samples. The discriminator is then required to decide whether the samples are real or fake. There is no way for the generator to know the completeness of its samples (how close they are to reality).
*Why is the dual input of real and fake data given to the discriminator?*
Because we need both to learn about the distribution. Providing just one will not give understanding about the other.
*If the generator becomes perfect, what will the discriminator output, and what does this imply about learning?*
If the generator becomes perfect, the discriminator should output 0.5. Why? Because it cannot tell whether it is real or fake. This directly means that the fake samples are similar to the real data. 
*Why is the GAN training described as a minimax game rather than a standard optimization problem?*
The generator and discriminator are opposing components. A standard optimization problem focuses on a singular minimization, whereas with GANs, the generator tries to minimizes the successes of the discriminator, and the discriminator tries to maximize its classification accuracy. This is the first case we have seen where is this dual-goal. 
*Suppose a GAN only learned a certain variety of images? What does this imply about the learned distribution?*
This indicates that the model has not learned the full distribution, or the distribution is not complete (has )

