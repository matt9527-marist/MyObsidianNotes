*Review the Following*:
![[Pasted image 20260312204430.png]]
- With supervised learning, we have a labeled data, and we can always evaluate our model.
- Unsupervised learning is unlabeled, and we have to search for the underlying main idea. 

**Generative Modeling**
![[Pasted image 20260312204628.png]]
We want to create a fake image, video, or text that looks real. How can we tell?
- It should follow the distribution of real data.

**Why Generative Models?**
![[Pasted image 20260312204649.png]]
Why do we want to create fake data? 
- Remember, this data is difficult for us to distinguish as fake from real. 
- We can use this as synthetic data to help in finding the underlying patterns in the real data. 

**Outlier Detection**
Both advantage and disadvantage. 
If through the generative models, we could learn about the "usual" distributions, they can help us catch the examples that are unusual or unpredictable. 
![[Pasted image 20260312204808.png]]
The disadvantage is that it is difficult for a model to determine what is real or fake (think the danger of self-driving calls)

**Latent Variable Models**
We want to extend what we have in autoencoders. We want to talk about variation on autoencoders. 