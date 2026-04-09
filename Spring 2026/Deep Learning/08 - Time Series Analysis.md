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

![[Pasted image 20260409190055.png|575]]
- Cross-sectional analysis: measuring the data at once time step. 
- Longitudinal data: measuring the data across several time steps. 

**Ordinary Regression Models**
In statistics, ordinary least squares (OLS) is a type of linear least squares method for estimating the unknown parameters in a linear regression model.
Simplest model we can use for this purpose:

$$Y = \beta_{0} + \beta_{1}X_{1} + \beta_{2}X_{2} + \dots + B_{k}X_{k} + \epsilon$$
**Simple Regression**
![[Pasted image 20260409190337.png]]
How do we find `b` the coefficients, how do we find the effective weights? 
- SGD - Stochastic Gradient Descent 

**Variable Types**
• covariate: A covariate is a variable that is possibly predictive of the outcome under study. A covariate may be of direct interest or it may be a confounding or interacting variable. The alternative terms explanatory variable, independent variable, or predictor, are used in a regression analysis. (Source: https://educalingo.com/en/dic-en/covariate) 
• confounder: confounding variable (hidden variable) is a variable that influences both the dependent variable and independent variable, causing a spurious association. (Source: https://en.wikipedia.org/wiki/Confounding 
	- Parameter that we don't measure, but it has effect in our outcome. Recall the *Hidden Markov Model*: we might need contextual information beyond what is strictly observed. For example, a person might take with them an umbrella when they decide to wear a coat, but the pattern is not there. The pattern is that it is raining. 
• Prognostic factors vs Risk factors (Souce: https://www.healthknowledge.org.uk/public-health textbook/research-methods/1a-epidemiology/sudies-disease-prognosis)

**The Problem of Multivariate Forecasting, like regression**
The difference between single variable and multivariate OLS is simply the presence of multiple inputs and multiple coefficients. 
• Covariates may not available all the time 
• There is a restriction 
• You do not know which covariates make y
![[Pasted image 20260409191336.png|487]]

**Autoregressive Models**
An AR model is one that `Yt` depends only on its own past values: `Yt-1, Yt-2, ...`
The model assumes that we have enough data to predict right now, without considering external factors. 
How many past values => `AR(P)`
$$AR(2) = B_{0} + B_{1}Y_{t}-1 + B_{2}Y_{t} - 2 + et$$
`et` is just white noise, which does not change over time. 

*White Noise*
`E(et) = 0`
`Var(et) = sigma^2`
Correlation between lags are 0. Lags are simply, how far do we look back? We expect that there are no patterns in the white noise between lags. This is also why we call it residual, as this will indicate if our model is missing an important pattern. 

**Auto Regressive Moving Average Model**
Auto Regressive Moving Average model (ARMA) represented as the past values and error term models: `ARMA(p,q)`
$$Y_{t} = B_{0} + B_{1}Y_{t} - 1 + \dots + B_{p}Y_{t} - p + et + \Phi*et-1 + \dots + \Phi*et - q$$
**Starionary of a Time Series**
 • Strictly stationary:
	 • Marginal distribution of Y at time t[p(Yt)] is the same at any other point in time
	 • Time invariant => mean and variances
	 • Differencing vanishing help us convert non-stationary to stationary to a stationary
$$d(f(Y_{1})) / d(y_{1})$$
![[Pasted image 20260409193024.png|585]]

$$ARIMA(p=3(Y_{t}? \leq Y_{t}-1,Y_{t}-2,Y_{t}-3), d, q)$$
I => Integrated 
In general a series which is stationary after being differentiated `d` times is said to be integrated of order `d`, denoted `I(d)`.

**Stationary Assumption**
It is very important form theoretical point of view since most standards methods are valid in stationary condition. Also, sometime OLS provide specious significant correlation.
![[Pasted image 20260409193450.png|474]]

**Box-Jenkins Methodology**
Trying a different technique to make predictions:
• It is a forecasting methodology based on:
	 • Identification
	 • Estimation
	 • Diagnostic checking
 1. Is it white noise => stop
 2. Stationary => do time-series analysis
 3. Non-stationary => do differentiation, return to 2

**Autocorrelation Function (ACF)**
![[Pasted image 20260409193729.png]]
Computes the difference between the lags. With `p` we are making a prediction some number of steps before. How many lags do we consider to make this prediction?
When we have such a plot, we will see a jump followed by a decline. This decides`p` for us based on the value that we have after the highest jump. 

**Advanced Time Series Predictions**
• Time Series Clustering
 • Time Series Classification
 • Hidden Markov Model (HMM)
 • Deep Neural Networks
 • Fast Fourier Transform