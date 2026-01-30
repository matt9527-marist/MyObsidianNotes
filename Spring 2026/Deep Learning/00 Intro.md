## Biological Neuron vs. Artificial Network 
![[Pasted image 20260122190546.png]]
Simplest element of artifical neural network is the *artificial neuron*, mathematically represented as a signal (inputs) into a specific function generating an output. 

> Perceptron - mathematical model of neurons in our mind. The most basic element in deep artificial neural networks 

![[Pasted image 20260122193847.png]]

AI is a large umbrella term. The hardware of AI includes machine learning, which is the "brain" that drives the AI. 
Deep Learning is a part of "representative learning" which attempts to learn from raw data. 

**Terminology**
AI definitions: (by the "fathers of AI")
1) John McCarthy: It is the science and engineering of making intelligent machines, especially *intelligent computer programs*. It is related to the similar task of *using computers to understand human intelligence*, but AI does not have to confine itself to methods that are biologically observable.
2) "Can machines think?" - defined by a question, offered by the famous *Turing Test*. 
	- Turing Test: Can the human, through sending and receiving messages from the robot, be convinced that the robot is human? 
3) We have 4 different definitions and goals for AI based on what we want to do:
	- Human Approach:
		- System that thinks like human 
		- System that acts like human 
	- Ideal approach: 
		- Systems that think rationally 
		- Systems that act rationally 
			- Why differentiate? For some tasks, we cannot define, clear-cut rational rules to provide the answer? For example, determine cat vs. dog given an image, and separate them. Such a simple task is still impossible to define a set of permanent rules for. The ideal approach may not be feasible, so we must go with the human approach. Then again, some tasks require a rational approach (factoring numbers)

## Early Successes of AI 
- IBM's Deep Blue chess-playing system defeated world champions in 1997. 
- Relatively sterile and formal environment- nothing they did not expect, a controlled environment. 
- Have to sought hard-code knowledge about the world in formal languages. 
	- A formal language is a set of strings of symbols drawn from a fnite alphabet in automata theory. 
	- Easier for a computer to understand, hard for a human to understand 
	- *Formal Language* is the understandable in-between, usually math and logic. 
	- *Hard-coding* means embedding data directly into the source code of the program as opposed to obtaining he data from external sources or generating it at runtime. If our chess opponent plays a certain position C11, for example, the system will play D11, placing action and effect together. 
- Abstract and formal tasks are among the hardest for humans to solve, but the among the easiest for computers to solve. 

![[Pasted image 20260122195918.png]]

## Why Machine Learning? 
• Moving from hard-coded knowledge to acquiring knowledge from raw data
• Accessing subjective and intuitive knowledge that are hard or impossible to
explain in formal language
• Capturing patterns through big, diverse, noisy, and missing data
![[Pasted image 20260122200329.png]]

**Definition for Machine Learning**
Arthur L. Samuel "Father of Machine Learning":
- Machine learning is the field of study that gives computers the ability to learn *without being explicitly programmed*.
Tom M. Mitchell
- *A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P if its performance at tasks in T, as measured by P, improves with experience E.*
- Experience E is basically data. Tasks T represent whatever objective we want with the data. Performance P can be measured in different ways (recall cost function/reward-punishments). Most deep learning algorithms will improve with more experience. 

**Types of Machine Learning Tasks:**
![[Pasted image 20260122201208.png]]

**Supervised Learning** (already in ML)
• Most supervised learning tasks fall under two umbrellas:  
*Classification* - We have the label for the instance. If the instance target is categorical, that is classification. 
*Regression* - If the instance target is numerical. Predicting a value. 
Classification and Regression.  
• Classification task examples:  
Image classification and diseases diagnostics  
• Regression task examples:  
Movies ranking and price prediction  
• Algorithm examples:  
K-nearest Neighbors, Linear Regression, Logistic Regression, Decision Trees  
and Random Forests, Artificial Neural Networks, Naive Bayes

**Unsupervised Learning**
We have a mixed input. Based on structure recognition, we want to separate the inputs. 
![[Pasted image 20260122201555.png]]

**Semi-Supervised Learning**
• Use unlabeled data around the labeled data as helpers to solve the task.  
• Semi-supervised learning task examples:  
Text document classification, speech analysis, and protein sequence classification  
• Sample algorithms:  
Transductive and inductive methods
![[Pasted image 20260122201639.png]]
- Consider the bias. The line separating the categories is determined by using unlabeled data to improve the analysis. 

**Reinforcement Learning**
• An agent observes the environment, selects an action, gets a reward, and  
updates its policy.  
• Task examples:  
Robot navigation, game AI, and self-driving car
- Use RL when we have a totally new task, knowing the target/goal, but *not knowing anything about the environment*. 
- Use RL when everything about the environment is known, but we do not want to waste our time searching the whole environment. 

![[Pasted image 20260122202131.png]]
*Uninformed Search* - No information will be given to me by conducting one action. 
*Informed Search* - Every action informs the next subsequent action with information.
- Binary vs. Linear Search 

Use RL: when the environment is known but is very big, or no information will be gained by taking an action. 

**Representation Learning**
![[Pasted image 20260122202718.png]]

![[Pasted image 20260122202800.png]]![[Pasted image 20260122202814.png]]

When should we deploy deep learning techniques?
![[Pasted image 20260122203040.png]]
Deep Learning (green) vs. Classic Machine Learning (yellow)

![[Pasted image 20260122203133.png]]

**Historical Trend of Growing Datasets**
- As of 2016, a rough rule of thumb is that a supervised deep learning algorithm will generally achieve acceptable performance with around 5,000 labeled examples per category and will match or exceed human performance when trained with a dataset containing at least 10 million labeled examples.
- With more computational power, there is the greater demand alongside this trend for high performance computing and more computational units for each algorithm. 

**High Accuracy vs. Interpretability**
![[Pasted image 20260129190528.png]]
Accuracy - shows the error reducing
But the seocnd image tells us that interpretability has an inverse relationship with accuracy. In the first layer, we can still make out the image, but in the last layer we cannot. 
There are attempts to add the interpretabilit
