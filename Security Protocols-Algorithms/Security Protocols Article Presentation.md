[Explainable Artificial Intelligence (XAI) for Malware Analysis: A Survey of Techniques, Applications, and Open Challenges](https://ieeexplore.ieee.org/abstract/document/10944807)
[Ransomware 3.0: Self-Composing and LLM-Orchestrated](https://arxiv.org/html/2508.20444v1)
## Introduction
The focus of this presentation is the duality of AI usage in modern cybersecurity subfields, particularly in the early detection of malware. Machine learning approaches to identifying malware have shown high accuracy, but there is one very significant problem at hand: 

> Early hook question for the class: "Has anyone ever had the misfortune of unknowingly downloading a malicious file, and suppose you were lucky to have Windows Defender flag it. Did you happen to get a message like this? # Trojan:Script/Wacatac.B!*ml"*

That `ml` tag at the end of the malware identifier means that Windows Defender used machine learning to classify the patterns it observed in the file as malicious. This is a good way of leveraging machine learning to help defend against security threats, and Windows Defender has been doing this for many years, but this alludes to the problem I mentioned:
- How do we verify that Windows Defender is classifying this file properly? 

