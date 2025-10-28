[Explainable Artificial Intelligence (XAI) for Malware Analysis: A Survey of Techniques, Applications, and Open Challenges](https://ieeexplore.ieee.org/abstract/document/10944807)
[Ransomware 3.0: Self-Composing and LLM-Orchestrated](https://arxiv.org/html/2508.20444v1)
# Explainable AI (XAI) For Malware Detection ML Models
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
> (Parallel to Kirchhoff's Principle)

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
	- **Local Explanation**: Focus on one particular instance instead of the overall model behavior. Lets us look at anomalies. There are two primarily used implementations:
		- LIME - (Local Interpretable Model-Agnostic Explanations) explains why a ML model made a specific prediction by using a smaller, surrogate model and slightly changing the input data that caused the prediction and observing how the prediction changes. 
		- KernalSHAP - model-agnostic, very computationally demanding (takes an exponentially long time to calculate SHAP values). 
			- Shapley Additive Explanations (SHAP) is a unified framework for interpreting machine learning models. It provides a way to understand the contributions of each input feature to the model’s predictions.
	- **Visual Explanation**: Produce visual representations of models that make them accessible and comprehensible. Convey model patterns using graphs or plots. 
		- Partial Dependence Plots 
		- Individual Condition Expectation 
- **Model Specific Explainability**: tailored to particular model architectures. 
	- TreeSHAP and DeepSHAP - Different approaches for optimizing SHAP calculation, one for tree-based methods and one for deep learning (neural network) models. 
	- Feature Relevance Explanations - methods used to measure feature importance (how much each feature/input contributes to a model's predictions), feature relevance, and how those features interact with each other (measured by the H-statistic). the entire SHAP family are examples of different feature relevance explanations (H-statistic - does changing one feature's value change the effect of another feature on the output?)
	- Saliency Maps - gradient-based methods designed specifically for neural networks, most commonly used in image classification, that show which inputs (such as pixels in an image) had the greatest influence on the model’s prediction

## Explainable Malware Classification and Detection Approaches
In the following section, the article summarizes several ways explainable AI can be applied to malware detections, organized by the type of target system. 
For the sake of simplicity, we will only be detailing the processes used for Windows PE (portable executable files), since that is likely what is most familiar to the class. This also makes sense since Windows is the most widely used desktop OS. 
There are three detection methods relevant for use here: 
1. Gradient-based 
2. Model-Agnostic 
3. Image-based 

### Windows PE File Malware Detection 
Windows .exe file format is base on "Common Object File Format" (COFF) specification: 
- File begins with a header used by the MS-DOS OS. 
- When loaded, MS-DOS checks for backward compatibility using a stub program.
- COFF header provides specs for the executable file 
- Section header divides the executable into segments, each comprising blocks of memory. This organizes the executable for more efficient execution. 
Despite Windows being so popular, limited research has been conducted on applying explainable machine learning frameworks to malware detection on Windows. 
An **opaque** model that we can look at is *MalConv*, an architecture that detects malware that takes as input the entire executable for a convolutional neural network (CNN). A CNN works by applying multiple layers of mathematical transformations to data. For MalConv, the data is not an image, as we might have seen CNNs more commonly used for, but instead a sequence of raw bytes from a given executable. 
- Convolutional layers detect small, local patterns
- Pooling layers compress the information, keeping the most important features and reducing noise. In this case, max pooling is used. 
- Fully connected layers combine all information learned to make a final decision. 
CNNs are a kind of "black box" model because humans cannot easily track how a pattern emerges as "important" within the model.

> How can we make clear the decision-making process of MalConv?

1. **Gradient Based Approach**: Use gradient analysis to define clear decision boundaries between categories (benign vs. malware). This allows us to define something like a heatmap for the CNN filters, which will allow us to view how the model determines a trait as being malicious in an executable. We can therefore pinpoint which segments or bytes of an executable are most influential for classification. 
2. **Model-Agnostic Approach**: Simplify the complex original model into a surrogate model. In one study, a system utilizes a variety of more transparent classifiers such as logistic regression or decision trees to detect malware based on memory dumps, in an attempt to approximate the processes used by MalConv. Explainability is further improved by SHAP, which gives us insight into the impact of each feature (DLLs, handles, kernel drivers, accessed services) on the prediction. 
3. **Image-Based Approach**: We know that CNNs are often used to classify images (identify letters/digits, cats vs. dogs). We can use this baseline with malware detection by converting executable binary files into grayscale images. By doing this, we can leverage CNNs' strengths in pattern recognition. By doing gradient analysis like in the first approach, we can then figure out which pixel regions most impact the model's predictions, and then security analysts can easily trace those regions back to individual snippets of code. 

One problem that we notice about the article is that it goes at length listing other studies doing indepdendent but relevant research. The article omits too many details for each approach, almost focusing on too broad of an audience. However, the goal is made clear. Each technique tries to balance interpretability, detection accuracy, and model complexity. 
## XAI Conclusions 
The article lists several ways by which research on this topic can be improved. The most critical points made are the following:
1. Improve Datasets: Malware detection datasets are limited or imbalanced. For example, a dataset for Android malware DREBIN has ~5,000 malware instances but 121,000 benign instances. This can hinder our ability to train effective models. 
2. Combine static and dynamic analysis: There exists a gap in research between using ML to analyze malware source code vs. malware actively running. 
3. Analyze Model-Agnostic Techniques: Automate explainability by further decoupling it from the underlying ML model. 
4. Apply Explainability Approach to Multiple Models
5. Use Pre-Trained Models
6. Improve Detection Efficiency: For example, improving the processing time for a decision tree by pruning or removing branches that do not provide enough information about an instance of malware. 
7. Mitigate Attacks: Stop threat actors from poisoning ML datasets or feature spaces. 
8. Hardware Malware Detectors: Further explore ways to leverage malware detection at the hardware level. 

The main idea that we can take away from this research is that while machine learning is a useful tool for cybersecurity, data-driven frameworks are vulnerable to exploitation, misdirection, and circumvention. 
**Transparency is a key requirement** for security experts to be able to trust and deploy these models. 

To further express the importance of this research, for the rest of this presentation, we would like to give the example of Ransomware 3.0.

# Ransomware 3.0 - LLM Orchestrated Malware 
## Introduction
A separate article listed on Arxiv by researchers at NYU discuss the evolution of ransomware over time. 
- Initial ransomware attacks going back to the well-known CryptoLocker, WannaCry, and Petya attacks utilized encryption schemes and gained access through phishing emails or vulnerability exploits. This is Ransomware 1.0.
- Ransomware 2.0 saw a paradigm shift where attackers not only encrypted the victim's data but also threatened to publish the data unless the ransom was paid. This also saw the creation of Ransomware-as-a-service (RaaS) where groups of developers generated ransomware payloads and sold them to buyers. 
- This brings us to **Ransomware 3.0**. We are in an age where software engineers are commonly consulting LLMs like ChatGPT in assisted IDE's like Cursor for writing code. How is this done?

## Threat Actor Assumptions and Objectives
Without going into too much detail, this second article assumes that an attacker has access to a target machine and is wanting to perform a ransomware attack. Instead of using RaaS, the attacker has outbound connectivity to an LLM service. They then proceed using prompts to have the LLM orchestrate the attack, including identifying sensitive data on the system to target and developing the payload. 
**Jailbreaking** - LLMs are restricted by their creators. You cannot tell ChatGPT to build a encryption payload for you for use in a ransomware attack. Threat actors can make use of *jailbreaking prompts*. These are elaborate requests made to the LLM to circumvent safeguards and ignore policies. 

![[Pasted image 20251027195645.png]]![[Pasted image 20251027195719.png]]

The article continues by describing an elaborate proof-of-concept ransomware construction pipeline that delegates all attack phases, including reconnaissance, encryption payload generation, and even ransom note creation to an LLM in real time.
## Conclusion 
From this summary of both research articles, we can see the dual-use nature of AI in cybersecurity. 
**Shared Theme**: XAI stresses the risk that AI can be exploited. That risk is laid out very clearly with Ransomware 3.0.
**Complementarity**: XAI provides transparency. Security experts need to understand how these models work in order to improve their ability to detect and prevent future threats that are supported by these models. 
**Conflicting Outcomes**: A lot of XAI methods offer post-hoc explainability. Ransomware 3.0 is real-time orchestration. It can make payloads polymorphic, meaning it can create malware that adapts itself to detection techniques and interpretability. 

We can expect AI to continue to evolve within the cybersecurity landscape. The key takeaway from this discussion is that, as future software engineers or security experts, we need to closely watch how new AI models are being developed and emphasize the importance of transparency and safeguards. 

##  Discussion Questions

> If we step outside of this topic as security analysts, what should the goal of future legislation be surrounding AI usage in cybersecurity? 
- If the audience says that AI as a whole should be restricted, stress that its evolution seems inevitable. It is already deeply embedded in our way of life. Is this really the solution?
- AI model production should have explainability enforced and there should be benchmarks in place that allow security analysts to test the performance of malware detection models using AI, in order to stay ahead of threat actors who are trying to do the opposite. 

> Why is AI-driven polymorphism a particularly worrying issue for malware detection? 
- The audience should surmise that malware rewriting itself at runtime breaks common static analysis patterns or signature-based detection. 
- Machine learning detection coupled wit XAI on features extracted from dynamic analysis sees a great use case here. 

> What is more important? Transparency in detection methods or accuracy and security in detection methods? 
- Can full transparency about how malware detectors operate inadvertently make them easier to evade?

> As AI is more commonly used in software development, where does human agency fall for snr