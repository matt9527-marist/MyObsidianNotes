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
