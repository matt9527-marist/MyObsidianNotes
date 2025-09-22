## Classication 
Suppose we have a classifier predicting a color of RGB:
`y = f(x) + c`
`y\hat = f(x)`
(see notes)
Relevant #Classification Metrics:
- **Accuracy** = # Matches / # Observations = 3/6 = 50% accurate
- **Error Rate** = 1 - Accuracy = 3/6 = 50% wrong

- **Confusion Matrix**:
(see notes)
	- Accuracy = Summation of Main Diagonal / Sum of All Cells 

**Binary Classification**
Why? This happens all the time and has become incredibly important in AI and predicting in several other fields. This is predicting YES/NO. 
In many situations, even if we have a case where there are more than 2 categories, we may end up wanting to subsume things into 2 categories regardless. 
Always a class value of interest:
- Detecting security intrusions: Threat or not a threat?
- Bank verifications: Valid or not valid?
- Disease Predictions: Disease present or not present?

- **Binary Confusion Matrix**
(see notes)
	- True Positive 
	- True Negative
	- False Positive 
	- False Negative 
Therefore our accuracy is:
$$Accuracy = \frac{TP + TN}{TP + FP + TN + FN}$$
This is the accuracy metric for a binary confusion matrix. While good, it comes with some drawbacks. Consider a case where a random classifier yields a very high `TN` count. For example, a classifier separating students who are doing well in college vs. students not doing well. 95% of the time, we will randomly select a student who is doing well. This metric will not yield us any good information about the classifier if this is true. We need other metrics. 

Other Metrics:
**Recall (True Positive Rate)**
$$Recall = \frac{TP}{TP + FN}$$
"Recall" comes from "information retrieval." This allows us to know how much data was captured that did not actually fly under the radar; how many times we correctly predicted fraud, an intrusion, or a disease, etc.

**False Positive Rate (FPR**
$$FPR = \frac{FP}{FP + TN}$$
This detects how many false alarms there were. There is a positive side of this called *specificity*, which is `1 - FPR`, in the same way that accuracy is a positive presentation of error rate. 

**Precision**
$$Precision = \frac{TP}{TP + FP}$$
True positives over all positive predictions. 
Remember that all of the above metrics are fractions. 

1) **F1 Measure**:
	$$F1 = 2\frac{Precision * Recall}{Precision + Recall}$$
	Range of F1 Score is between 0 and 1. 
	1 indicates much better performance, 0 is disastrous. 
2) **ROC** - Receiver Operator Characteristic **Curve**
	Using probabilities to assign 0 or 1. 
	(see notes)
	
	Depending on the thresholds we assign (risk), a perfect classifier is one that traces the left and top line as shown. We may also use the space underneath to tweak other models, allowing for a little bit of false positive predictions, but keeping a high true positive rate. 
	- The total area under the top curve is 1.
	- The area underneath the main line is 0.5, which indicates a crappy classifier. 
	The area under the curve of the ROC curve is referred to as **AUC**. 
	This does have one problem!
		If the data is highly unbalanced, AUC tends to have inflated values. Keep in mind that FPR carries the true negatives that may be unbalanced in the data. 

## Probability 
#probabiliy is a measure of uncertainty where:
`0 <= P <= 1` where 0 is not possible and 1 is certain. 
Before speaking in terms of **Bayesian** probability, we have approaches:
- **Natural**: Ratio between events / event space 
- **Frequentist**: Repeated trials 
- **Bayesian**: If we cannot repeat trials, we must assume we have *prior knowledge* about the world. We can use this prior knowledge to inject it into the data we have. Now this becomes our new prior information, and then we repeat. 

Axioms to Consider:
1) **Sum Rule**: $$P(A) + P(B) + P(C) = 1$$ where A, B, C mutually exclusive and collectively exhaustive. 
2) **Product Rule**: $$P(A, B) = P(A|B) * P(A)$$
3) Given that P(A,B) = P(A|B) * P(B) = P(B|A) * P(A) (symmetrical)
   We obtain that $$P(A|B) = \frac{P(B|A) * P(A)}{P(B)}$$
    Consider the following problem:
	We are pulling out of a hat A's and B's. What's the probability of getting an A and a B when there are 3 A's and 2 B's in the hat?
	--> We first retrieve a B. The probability of getting a B was 2/5.
	--> We put the letter aside. It is no longer in the collection. 
	--> The probability of getting an A is conditioned on the removal of B from the lot. This is now 3/4.
	The product rule is saying that the *joint probability* of these two events (getting an A and getting a B) is given by, assuming that we get a B initially, `3/4 * 2/5`
	
	Suppose we change the scenario:
	When A and B are independent, `P(A, B) = P(A) * P(B)`. This assumes we put the letter B back into the lot.


