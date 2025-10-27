[Explainable Artificial Intelligence (XAI) for Malware Analysis: A Survey of Techniques, Applications, and Open Challenges](https://ieeexplore.ieee.org/abstract/document/10944807)
[Ransomware 3.0: Self-Composing and LLM-Orchestrated](https://arxiv.org/html/2508.20444v1)
## Introduction
The focus of this presentation is the duality of AI usage in modern cybersecurity subfields, particularly in the early detection of malware. Machine learning approaches to identifying malware have shown high accuracy, but there is one very significant problem at hand: 

> Early hook question for the class: "Has anyone ever had the misfortune of unknowingly downloading a malicious file, and suppose you were lucky to have Windows Defender flag it. Did you happen to get a message like this? # Trojan:Script/Wacatac.B!*ml"*

![[Pasted image 20251008152032.png]]

That `ml` tag at the end of the malware identifier means that Windows Defender used machine learning to classify the patterns it observed in the file as malicious. This is a good way of leveraging machine learning to help defend against security threats, and Windows Defender has been doing this for many years, but this alludes to the problem I mentioned:
- How do we verify that Windows Defender is classifying this file properly? 
- How can we interpret the results of the detection beyond the tag in order to better mitigate future similar threats? 

Think about this in terms of a different field. For example, in *healthcare*, medical professionals might rely on predictive ML models, but those come with the possibility of incorrect predictions. If it is a **black-box** model, how can the healthcare professional be sure that say, a cancer diagnosis is a correct prediction? Same thing for malware, how do you know if that flag given by Defender is actually a trojan? And if it is a trojan, how does it know? What does it do?

> This is the issue with **black-box** models. This means that the internal decision making or data transformation process is obscured or at least not easily interpretable. Examples include Random Forest models, neural networks, or even LLMs like GenAI. Think about how ChatGPT sees billions of parameters interacting in nonlinear ways, making it nearly impossible to trace how specific parts of an input text influenced parts of the output text. (show diagram)
> 
> This is as opposed to **white-box** models, which includes linear regression, decision trees, or rule based systems, where we can clearly see or understand how certain inputs map or are transformed into outputs or predictions.

What IEEE is advocating for through this article is to make **transparency** a prerequisite for malware detection and analysis models. 

We will also be later discussing Ransomware 3.0, which is the reverse narrative that we bring to this presentation, where, without transparency, AI and machine learning becomes its own potentially uncontrollable attack vector.

## How Malware is Detected
Let us first explain modern malware detection techniques. These are categorized into 2 distinct approaches: 
1) *File Classification*
	- File classification looks at the file's code to check if it is malicious. There are three ways this is done:
	1) Static Analysis: examine the code without executing the file. This usually uses a signature-based approach to extract suspicious features in the code. This can include specific API calls, instruction opcode sequences, or n-grams identified from known suspicious files. While useful, static analysis fails to catch more complex or new malware that needs to be running on a system to see its effects. 
	2) Dynamic Analysis: execute the code in a closed environment to see what it does. Here, we can compare system call patterns and memory usage between benign and malicious programs. The issue here is that this can be time and resource expensive. 
	3) Hybrid Analysis: combine the above two approaches. There is a website that does this for us: [Free Automated Malware Analysis Service - powered by Falcon Sandbox](https://hybrid-analysis.com/)
2) *Online Detection*
	- Focuses on the behavior of the entire machine rather than individual malware behaviors, which enables us to capture malware in real-time, regardless of its specific activity level. 

In practice, these detection approaches show some patterns on which we can train ML algorithms. System calls for example, in dynamic analysis, can be a key feature or attribute that identifies a file as malware, so we might say that feature holds a lot of weight in decision tree or neural network. 

## Explainablity in Machine Learning 
This is brings us to the issue at hand: the reasons for why AI outputs something is not interpretable by humans. Lots of ML algorithms are a black box, like we said, where we cannot easily comprehend what patterns or what weights an algorithm is assigning to a certain variable to make a prediction. 

![[Pasted image 20251020190944.png]]

> How can we trust systems that we cannot explain? 

Explainable AI (XAI) is suggested by the article as one method by which we can obtain clear justifications from a model on why it makes certain predictions. 
XAI is meant to be *accurate* in its ability to generalize on new data, in this case, new malware or unseen programs. We should be able to assign a degree of *fidelity* depending on how the model justifies its prediction. Predictions and explanations for predictions should be *consistent*. 
We should be able to derive *degree of importance*, meaning we should be able to learn how much weight a model assigns to a certain feature. 

These aspects of XAI are proposed by IEEE to improve trust and hand the regulatory power over AI back to humans.
## Transparent vs. Opaque Machine Learning Models 
**Transparent Machine Learning Models** are inherently explainable, typically not requiring post-hoc explainability techniques.
**Opaque Machine Learning Models** are highly accurate but complex and difficult to explain. It is challenging for a human to understand the patterns that the model is predicting upon, or there are layers of computation being performed by the ML algorithm that are not intuitive. 

![[Pasted image 20251020194133.png]]

There is no need to fully describe each of these models, but we will give an adequate breakdown of just two of the models for each of the two categories: transparent and opaque. 

### Transparent Models

**Regression Models** - This includes linear and logistic regression. These models are inherently very explainable.
![[Pasted image 20251020195315.png]]
The structure of this model has a simple additive equation consisting of weights that are easily quantifiable. 
$$y = w_{1}x_{1} + w_{2}x_{2} + w_{3}x_{3} + \dots + w_{n}x_{n} + b$$
- `w`'s are the weights given for each `x` feature in a given dataset. What we are determining with the above expression is how much `y` changes when  `xi` changes by one unit. 
- We can easily understand and visualize this equation. The weights themselves can be listed in a table. The simplest representation of the model is basically a line of best fit. 
- There is no layering or hidden weights. 

**Decision Trees** - Also inherently explainable and can be visualized very easily. 
![[Pasted image 20251026181653.png]]
Decision trees are composed of "branches" that stem from conditional `if-then` rules. Binary decision trees like the one shown above resemble how humans logically think through problems. 
- The key is that the **structure is the model**. There is no hidden computation, just rules that when followed lead down to intermediate conditions or a prediction. 
- Domain experts can follow the same decision-making process that the tree follows, leading them to the same conclusions as the model. 

### Opaque Models 
**Random forests** - An ensemble of many decision trees whose predictions are averaged or chosen based on majority vote to determine the output conclusion. 
![[Pasted image 20251026183416.png]]
There is a notable disconnect here compared to just a single decision tree. 
In a single tree: 
> The model predicts on a series of if-then rules: 
> 	if known malicious API calls < 30 and REG_KEY created == FALSE
> 	then prediction for process is not malicious 

In an ensemble of trees (random forest): 
> Hundreds of trees make different decisions on the features in a given sample.
> 	Tree 1: Malicious (based on API calls)
> 	Tree 2: Benign (based on network behavior)
> 	Tree 3: Malicious (based on file entropy)
> 	... 
> 	327 trees say malicious
> 	173 trees say benign 
> 	Final decision -> Malicious by majority vote 

As we can see, the process for a human to trace the decision-making through the model is a lot more obscure. No single interpretable rule path explains why the ensemble arrived at its conclusion. 

**Deep Neural Networks**: In the same way that a human cannot trace the decision-making path for a given output through a random forest, it is very difficult to explain the same through a neural network, especially when there are several layers. 

These models are also computationally intensive with a lot of internal mechanisms that lead to answers. You can certainly ask ChatGPT for example to give a reason why it outputs something, but that still does not let us know the actual weights and factors that are being considered internally. 

## Post-Hoc Explainability 
These are methods that allow us to interpret opaque, complex ML models' predictions, especially in high-stakes applications where transparency in decision-making is required. There are two ways to do this:
- **Model-Agnostic Explainability**: applicable to any model 
	- **Global Explanation**: Look at all instances instead of individual predictions. This lets us determine which features are relevant on a systemic level. 
		- Use *surrogate models*. These models approximate the decision-making process of an opaque model by training an interpretable alternative (decision tree or linear model). Adds explainability by allowing us to pinpoint how important a given feature is in determining malware (API calls or file metadata for example). However, is limited because they are just approximations/replications of the full opaque model. 
	- **Local Explanation**: Focus on one particular instance instead of the overall model behavior.
- **Model Specific Explainability**: tailored to particular model architectures. 
