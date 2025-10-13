## Support Vector Machines (SVMs)
#SVMs
Within the realm of linear classification. 
	The work of two Russian theorists: Vapnik and Chervonekis. This work falls under what can be called the VC Dimension (1996)
The goal is to find the optimal VC:
	If your VC is too low, the model has too much bias and underfit. 
	If your VC is too high, the model will have high variance and overfit.
*An SVM training algorithm builds a binary classification model.*

How do we characterize VC's?

**Maximum Margin Binary Classifiers** (1990s):
We need some theory: 
- Recall: The equation for a **hyperplane**:
(see notes)
In this case, we are describing a line. This is visualized in 2D for simplicity. 
Pay close attention to the expression:
$$w_{1}x_{1} + w_{2}x_{2} + b = 0$$as it will return repeatedly throughout this topic. 

Imagine the following:
(see notes)
The two lines represented by the differing intercepts `b1` and `b2` are parallel. That is, their slopes are the same, but the intercepts can change. 
We want to compute `d`, the distance between the two parallel lines. 

