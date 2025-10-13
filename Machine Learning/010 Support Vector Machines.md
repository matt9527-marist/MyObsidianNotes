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

*Equation of a Hyperplane*: $$w^Tx +b = 0$$
*Distance between two parallel lines*: $$d = \frac{|b_{1}-b_{2}|}{||w||}$$
With these fundamentals, let us return to the topic of classification:
We may have the following situation: 
(see notes)
**Linearly Separable** problems are ones where the two classes of data points can be separated by a straight line. 
But see the diagram, you should ask yourself, "is the plotted line the best possible line?"
There are really infinitely possible separation lines. 
We need to be able to draw lines such that the separation between the classes is as wide as possible. This is called an *avenue*. Therefore, we need to find the points on which to plot lines that maximize the width of that avenue. 

To define the avenue, we need to define the sides and identify the middle of the avenue. The middle of the avenue can be defined, as we know, as $$w^Tx + b = 0$$where anything above this center line will be classified as the +1 region, and anything below will be classified as the -1 region. 
Without loss of generality, just by tweaking the values of `w` and `b`, we can easily say that the line defining the upper side will be: $$w^Tx + b = +1$$and the line defining the lower side will be: $$w^tx + b = -1$$
Now that we have these formulae, we need to compute the distance `d`, ie. find the `w`'s and `b` that maximize this distance `d`