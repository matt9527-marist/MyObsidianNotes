# Machine Learning

Relevant libraries:
- *[Numpy](https://numpy.org/doc/2.3/user/basics.creation.html)*
- Matplotlib (Graphing/Charting)
- *[Pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/index.html#user-guide)*
- **Scikit-Learn***
- **Keras***
- **TensorFlow***

Relevant Reading Materials:
- [Statistical Learning](https://web.stanford.edu/~jurafsky/slp3/)
- ISLP - Statistical Learning and Applications with Python
 
---

## What is Machine Learning?

**Field of study giving computers the ability to learn without being explicitly programmed**
- Detecting patterns and regularities with a good and generalizable approximation("model" or "hypothesis")
- Execution of a computer program to optimize the parameters of the model using training data or past experience.

![[Pasted image 20250825170340.png]]

Modern AI is mostly data-driven. 
Most of machine learning can be simplified to a optimization problem, often using a dataset to predict something in the future. We want that prediction to be as accurate as possible. 

*A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.*

Task T: recognizing and classifying handwritten word  
Performance measure P: percent of words correctly classified  
Training experience E: a dataset

![[Pasted image 20250825170834.png]]

**Optimziation**:
We set a goal, we feed the leanring model data, and try to reach some kind of minimal value. 
We are trying to minimize the error of the model between the ground truth about something and its prediction. 

Examples:
✓ Control theory (minimize a  
cost function)  
✓ Economics (maximize  
expected utility)  
✓ Operations Research  
(optimize objective  
function)  
✓ Statistics (minimize loss  
function; ML borrows this)

![[Pasted image 20250825171112.png]]

Mostly we discuss everything surrounding supervised learning. 
**Supervised Learning** - Regressing or classifying? Making a prediction on a descript target or a numerical target? 
There are various classes of predictions. For example, we may have a medical model make a *binary* yes or no prediction on whether an observed input image of tissue mass is cancerous. 
- There is of course the issue of dimensionality reduction. How high definition of an image would the model need? We may not need every single pixel of that image to represent a feature. 
**Reinforcement Learning** - Not our focus, but is poignant. Google's Deepmind winning games against humans using reward-based decision processing to learn series of actions. 

## Supervised Learning

#SupervisedLearning
The ML system learns patterns and relationships from large amounts of data to make predictions. 
![[Pasted image 20250825172007.png]]
Find a way to minimize the cost function, which may be a sum of all errors or a number of other possible error accumulation functions. 
Once we have a trained model with what we want, we test it with newer inputs. 
The quality of the algorithm depends on how well we are able to capture the features out of the data we already have. 

**Training example**: A row in the table  
representing the dataset. Synonymous to an  
observation, training record, training  
instance, training sample (in some contexts,  
sample refers to a collection of training  
examples)  
**Feature**: a column in the table representing  
the dataset. Synonymous to predictor,  
variable, input, attribute,  
covariate.  
**Targets**: What we want to predict.  
Synonymous to outcome, output, ground  
truth, response variable, dependent  
variable, (class) label (in classification).  
**Output / prediction**: use this to distinguish  
from targets; here, means output from the  
model.

We will make use of the popular Iris Dataset:
![[Pasted image 20250825172207.png]]
With these morphological elements, we are able to make predictions on the type of Iris. 

**Instance** x (boldface ==> vector)
Set of n instances:
![[Pasted image 20250825172310.png]]
Instance as a feature vector, with m features:
**x** = (x<sub>1</sub>, x<sub>2</sub>, ..., x<sub>m</sub>)
![[Pasted image 20250825172417.png]]

Common Example of Supervised Learning:
Self-driving cars:
![[Pasted image 20250825172751.png]]

## Unsupervised Learning

![[Pasted image 20250825173041.png]]
(Principle Component Analysis)
![[Pasted image 20250825173048.png]]

Let us assume that we bring in a set of individuals, let's say a mix of males or females. Initially, however, we know NOTHING about them. Suppose we take some measurements, and we end up with 3 separate categories according to what affinity features each individual corresponds to. 
This is *clustering*, which is much of data mining task.

Unsupervised learning is meant to *discover interesting structures* from data, not being told what the intended output is.

## Reinforcement Learning
Learning system called the *agent* in this context, can observe the environment, select and perform actions, and get *rewards* in return or *penalties* in the form of negative rewards. It must then learn by itself what is the best strategy to achieve the goal or perform the desired task. 
![[Pasted image 20250825173609.png]]
Example: Atari Breakout Game was beaten by a reinforcement learning model. 

> **No Free Lunch Theorem** (NFL): The only way to know for sure which model is best is to evaluate them all. There is NO perfect algorithm/universal algorithm that will address any different dataset that we want consider. Because it is not possible in practice to do this, we are forced to make some reasonable assumptions about our data and evalute only a few most reasonable models. 

**Optimization Methods**
In some cases, we may be doing combinatorial search, greedy search (decision trees), convex optimization (least squares), SVMs, Backpropagation, chain rule (neural networks), Constrained nonconvex optimization. 
There is a connection between these methods. At the end of the day, we are simply searching for a good way to minimize some error. 

**Loss Function**
The function we are minimizing. The loss function, often called error or cost function, measures the difference between the ground truth and the prediction we are making.

**Other Relevant Metrics**
• Squared Error/MSE / MAE (regression)  
• Cross Entropy (classification)  
• Hinge loss  
• Entropy (DT classification)  
• Gini Index (DT classification)  
• Regression metrics  
	– MSE / MAE  
• Classification metrics  
	– Accuracy (1-Error)  
	– Recall / FP Rate / Precision /ROC AUC  
	– Maximum Likelihood / MAP

Five Tribes of Algorithms:
![[Pasted image 20250825174542.png]]

Returning to the initial question:
IF human intelligence is defined to the extent that humans' actions can be expected to achieve humans' objectives, AND machines are intelligent to the extent that their actions can be expected to achieve their objectives, what is the problem?
- The objective of the machine should be related to the objective of the human.
- But what if the developer of the machine did not align the machine's goals with that of the human?
- This comprises a philosophical moral problem when the goals of the machine differ from the goals of the human. 

There is also the issue of **hallucinations**. The models we have today are trained to please the prompter. LLMs can present completely false data or fabricate papers/articles to satisfy the prompter. 

