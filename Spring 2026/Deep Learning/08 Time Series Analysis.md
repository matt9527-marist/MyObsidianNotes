What do we want to do with a time series?
![[Pasted image 20260409184415.png|632]]
Time series applications and context:
- Making predictions 
- Anomaly detection 
- Counterfactual prediction (if we do something, how will it affect the future?)

![[Pasted image 20260409184548.png|527]]

**Terminology**
*Systematic* vs. *Non-Systematic*:
- Systematic: components of the time series that have consistency or recurrence and cna be described and modeled. These elements can be extracted from the time series that help us to capture the general pattern. 
- Non-Systematic: Components of the time series that cannot be directly modeled.

![[Pasted image 20260409185341.png]]
What patterns can we notice about this time series?
- It is increasing over time. Perhaps air travel and technology is improving so there is more air travel?
- If each spike is occurring within a year, that spike can indicate holiday periods or frequent vacation periods where people are traveling a lot. 

**Time Series Components**
A given time series is thought to consist of three systematic components including level, trend, seasonality, and one non-systematic component called noise. These components can semantically defined as follows: 
	• Level: The average value in the series. 
	• Trend: The increasing or decreasing value in the series. 
	• Seasonality: The repeating short-term cycle in the series. 
	• Noise: The random variation in the series.
![[Pasted image 20260409185552.png|371]]
*Goal*: We want to extract a pattern from the data. A successful model here is indicated by the lack of any pattern in the residual.
We should not see any patterns in the residual.


