### Intro 

**AI Definitions**
There is the ideal/rationl approach and the human approach:
- Ideal Approach:
	- Systems that act and think rationally
	- Where we can finitely describe the set of rules 
- Human Approach: 
	- Systems that act and think like humans 
	- Where we cannot define the specific set of rules 

**Early Successes of AI**
Starting from sterile environments (Chess or simple games) absorbing the state space to beat humans. 
- Hard-coding: embedding data into the source code. 
- All of the knowledge base is the repository of domain knowledge and meta knowledge, but they embedded data and knowledge together. 

**Why do we need machine learning?**
- Learn the knowledge from the raw data. 
- Giving the computers the ability to learn without being explicitly programmed. 
- *A computer program is said to learn from Experience E with respect to some class of tasks T and performance measure P if its performance in tasks T, as measured by P, improves with experience E.*
	- If we change the task or performance measure rapidly, it means that the system is not designed to be successful, but it specifically will be hard-coded to work for a certain matter. 

![[Pasted image 20260507184837.png|433]]

**When to use Reinforcement Learning**
- When facing a new environment where we have no knowledge of the outcome. 
- Where, in games, we have a wide variety of actions and states, where the computation of it is very costly.  We know the goal, but we need to explore the environment to reach it. 

*Rule-based Systems*
- Input --> Hand-Designed Features --> Output 
*Classic Machine Learning*
- Input --> Hand-Designed Features --> Mapping from Features --> Output 
*Representation Learning*
- Input --> Features --> Mapping from Features --> Output 
- Input --> Simple Features --> Additional layer of more abstract features --> Mapping from features --> Output 
(Hand-Designed Features: we are the ones computing the features)

**When to apply deep learning techniques**
When we have unstructured data, nonlinear relationships, with a need for high accuracy. 

### Multi-Layer Perceptron (MLP)
Each layer is FULLY CONNECTED to all perceptrons in adjacent layers. 
- We start with a specific input X.
- Different perceptrons are connected together with randomly initialized weights. X is passed through those perceptrons to obtain a prediction. 
- Our loss function is used to define the error / score between the target value (true) and the prediction Y.
- Use an optimizer (Adam) to perform a weight update using the loss score. 

**Forward Propagation**
Pass the input and make a prediction. 
Uses nonlinear activation functions. A combination of linear activation functions would still be a linear decision boundary. Nonlinearity is REQUIRED to model complex patterns. 
- Each activation function has major characteristics:
	- differentiable
	- 0-centered 
- Each has its own advantages and disadvantages:
	- Sigmoid has a clear decision boundary bounded between 0 and 1 (good for binary classification or probability), but suffers from vanishing gradient problems.
	- ReLU reduces the problem of vanishing, but it has the problem of steadily increasing the error, which is why we want to use Leaky ReLU, to sustain negative updates.

*The most efficient network* is the one that demands the least computational time and power while providing the highest accuracy.

**Data Splitting**
- Training is the data we are directly using to train the model. 
- Validation is the data used to measure the bias of the fitted model to the training dataset, giving an estimate of overfitting. 
- Testing is the data we use to evaluate the performance of the model.

**Stochastic Gradient Descent (SGD)**
Find the network weights to achieve the lowest loss. 
- Stochastic gradient descent allows for the samping of batches of data points to compute the gradient loss. 

**Batch Size**
As our batch size becomes larger, we will converge to a sharp minimizer, so we will have weaker predictions. We want something that is smoother. There is also higher computational cost. 

**Feature Scaling**
Without properly scaling, we may end up in a zig-zag learning pattern, since the data might not be normalized around 0. 

**Batch Normalization**
Feature scaling is good, but we may still see the shifting in the dsitribution of data as we move between the layers. 
It's good to put BN() after fully connected or convolutional layers, but before nonlinearity. 
BN() reduces the chance for an internal covariate shift, which slows learning by forcing the hidden layers to learn to adapt to the new distribution. 

**Underfitting vs. Overfitting**
Consider why we use Early Stopping:
After a certain point in training, if we see the validation error going up, it means we are no longer learning the general pattern, but we are memorizing the data. This causes overfitting, so we want to stop training right as we reach this point. 

*For each different problem*, we may need a different activation function, proper loss function, or suitable optimizer. 

### CNNs

Instead of a multi-layer perceptron, we just connect each perceptron to only a WINOW of layer parents and children. CNNs have LESS complexity than MLPs. 
- Gives us the ability to find the pattern wherever it is located in an input. 
- For an image, the object of interest does not need to be centered, whereas with an MLP, it needs to be in the same consistent position. CNNs can magnify and find that object because they have *translational* or *spatial invariance*. 

### RNNs 

Our most complex form of MLP, it keeps a history of itself. 

We have different RNN types:
![[Pasted image 20260507192304.png|539]]

Two specific versions of RNN:
GRU and LSTM:
- These are **Gated RNNs** which use a set of gates on information flow to control how much information is remembered from the past or added to memory/discarded from memory.

**Bidirectional RNN**
- Each layer is not limited to pass data only to the next layer. It can also pass layer to the second or third layer. 
- Can be connected to different layers. 

**Attention Mechanism**
Allow us to focus on a specific part of the data or image. 

### Involutional CNNs

We can have different dimensions of CNNs. 
- Time series of single input (1D)
- Pictures with a singular channel (2D)
- Colorful image (3D) 

**Involutional CNNs**
These CNNs try to not only consider the elements that are besides each other, but also consider what is happening through each block, thereby seeing more context. 

**Separable Convolutional Network**
Separate the kernels to have faster computation. 

### Autoencoders 
Mapping an input to itself:
- Create a **latent space**
- Compress the data and also find the concept/meaning of the data. 

### Generative Models 
Generate some outcome by extending *autoencoders* to *variational autoencoders*.
Through variational autoencoders, instead of simply finding or creating the latent space, we find the **distribution** behind that latent spacec (standard deviation and mean).

We describe the loss and regularization terms:
1) *Continuity*: Points that are close in latent space map to similar content after decoding 
2) *Completeness*: If we choose any random value in our latent space, we want it to be meaningful content after decoding. 
Encoding a distribution does not preserve these properties! 

**Latent Space Disentanglement with B-VAEs**
Enforce that we are learning the pattern:
![[Pasted image 20260507193213.png]]
Consider that the rotation of the head must also match with the face smiling. 

**GANs**
Generative Adversarial Networks: 
![[Pasted image 20260507193323.png]]
Have a generator competing against the discriminator. 
We would like the discriminator's accuracy to be around 50%, indicating that it cannot differentiate the real data from the fake, generated data. 

**Conditional GANs**
Add a conditioning factor that controls the nature of the output. 
Changing the environment. 

**CycleGANs**
Move our input into another domain with unpaired data. 

### Time Series Analysis 
A useful abstraction for selecting forecasting methods is to break a time
series down into systematic and unsystematic components.
	• Systematic: Components of the time series that have consistency
	or recurrence and can be described and modeled.
	• Non-Systematic: Components of the time series that cannot be
	directly modeled.

These components can semantically defined as follows:
• Level: The average value in the series.
• Trend: The increasing or decreasing value in the series.
• Seasonality: The repeating short-term cycle in the series.
• Noise: The random variation in the series.

**Different Applications for Time Series Analysis**
*Payment Card Fraud*: Use a standard dense Keras model that performs a classification (fraud or no fraud)
*Weather Prediction*: Use an LSTM to track long-term dependencies like seasonality. 
*Anomaly Detection*: Use a CNN to detect the object of the anomaly, seeing the input data as an image. 

### Deep Reinforcement Learning 

Elements of an RL problem:
- agent
- environment 
- state 
- action 
- reward
- total return 
- discount factor 

For a given problem, we may define a **Q-Table** of different action and state mappings. 
Define a *Q-Function* that can determine what the best action is at a given state. 

**Experience Replay**
When we observe a similar state with the same action that we have already seen, we want to sample from replay memory to reuse the same solution instead of computing it again.

### NLP 

Complex problem that depends on the meaning and context of words and phrases. 

**WordNet**
- provides one singular meaning for a word
- But words can have several different mearnings 
We move to the algorithm **Vectorization**

**Word2Vec**
- Capture the meaning of the words, where words with similar meaning have similar vectors.
