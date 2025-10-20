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
