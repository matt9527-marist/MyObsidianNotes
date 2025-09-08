*Problem:* how to improve the sales of a given product 
*Data*: advertising data set consisting of the sales of the product in 200 different websites. This comes from 3 sources of advertising: TV, radio, and newspaper. 
*Goal*: develop an accurate model that can be used to predict the sales on the basis of those 3 markers. 

![[Pasted image 20250908153844.png]]

This is supervised learning:  
1. Collect training data  
2. Use a learning algorithm to fit a model  
3. Use model to make a prediction

![[Pasted image 20250908153922.png]]
The advertising budgets are  
input variables while sales  
input is an output variable.  
✓ Sales= f(Radio, TV ads )

We assume that there is some relationship between the output variable 𝑦 and the input variables denotes as a vector 𝐱 = (𝑥<sub>1</sub>, 𝑥<sub>2</sub>, . . , 𝑥<sub>𝑚</sub> which can be written in the very general form.
𝐱 represents the possible media sources, which = 3

	y = f(x) + e

Why *"+ e"*? We have a target and some fixed formula on that target to produce a solution, but perhaps we have some errors or missing data. Perhaps we need more variables or components in our vector 𝐱 to fully determine the function. We need some variation to take this into consideration. 

- *f* is fixed but unknown function of 𝐱.
- Assume error represents some noise with some variance. 
- *f* represents the systematic information that x provides about y. 
- However, *f* is **generally unknown**.
- In this case, one must estimate *f* based on the observed points. 

![[Pasted image 20250908154630.png]]

We fit *f*^(x;D) as the best possible by minimzing the mean squared error (MSE)
![[Pasted image 20250908155000.png]]
This kind of measure is a **cost function**. 
This is trying to measure the error between all the data points and the model attempting to predict *y<sup>^</sup>*. 
![[Pasted image 20250908155945.png]]

## Regression and Prediction
In any supervised model that we develop, we will train the model on some dataset that we have collected, but will always try to set aside a certain portion of the original dataset to be used for *testing purposes*.
This is the general idea of **splitting the data**.

We want the 𝑴𝑺𝑬 to be minimal for dataset 𝑫 (to find  
the best fit) and points outside the sample (in the latter,  
for accurate prediction purposes)

This means that we minimize 𝑀𝑆𝐸 on training data D to  
optimize the fit, and assess the effectiveness on points  
outside the sample by computing 𝑀𝑆𝐸 on test data (same  
formula, different dataset)![[Pasted image 20250908160116.png]]

This is to ensure that the model is capable of *generalizing* its predictions beyond the data it has been presented. 

**Two Sources of Erorr in our Prediction**
Of course, we cannot hope to fit the function perfectly to y, since 𝑦 = 𝑓(𝐱) + 𝑒 contains noise e.
Even if we were to form a perfect estimate for *f*, so that the estimated response took the form y^ = f^(x), our prediction would still have some error!
	y is also a function of error e, which, by definition, cannot be predicted using x. 
	Therefore, variability associated with e also affects the accuracy of our predictions. This is known as the *irreducible error*.
Also, f^ will not be a perfected estimate for *f*, and this inaccuracya will introduce some error. This is known as *reducible error*.
The accuracy of 𝑓(𝐱;𝐷) as an estimate for 𝑦 therefore depends then on two quantities, the reducible error and the irreducible error.
![[Pasted image 20250908160318.png]]
Two important points to consider: **bias** and **variance**. 

