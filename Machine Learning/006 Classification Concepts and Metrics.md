## Classication 
Suppose we have a classifier predicting a color of RGB:
`y = f(x) + c`
`y\hat = f(x)`
(see notes)
Relevant Metrics:
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
This is the accuracy metric for a binary confusion matrix. While good, it comes with some drawbacks. 



