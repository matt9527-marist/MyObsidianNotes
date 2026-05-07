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

