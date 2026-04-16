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

**Performance Summary**
![[Pasted image 20260409194038.png|649]]

**Deep Learning Time Series possible objectives**
![[Pasted image 20260409194217.png]]

**Time Series Classification**
![[Pasted image 20260409194953.png]]
Example: binary classifier (YES | NO) for determining credit card fraud:
We can use a standard Keras model with a dense layer output of 1. 

**Time Series via LSTMs**
We want to make a prediction with weather:
![[Pasted image 20260409194828.png|288]]
We can very clearly see the effect of the *seasonality*. Long-Short Term Memory is great for capturing this distribution over time. 

**Time Series Anomaly Detection**
![[Pasted image 20260409195037.png|602]]
Why did we not go with the LSTM or another model here? 
- Remember the purpose of using an autoencoder. 
1) Cost:
	- What was the cost of the different layers that we have? 
	- RNN > MLP > CNN
	- CNN here is better.
2) Objective:
	- Find specific events. 
	- Our goal is not to find the pattern, since we are not trying to make a prediction using the seasonality or trend. 
	- When we want to find a specific event that is deviating from the rest, we just want to pick up that object. This model will magnify that event, using convolutional layers. The data can still be viewed as a picture. 

**How such a model can be helpful**
 • Model usage:
	 We will build a convolutional reconstruction autoencoder model. The model will 
	take input of shape (batch_size, sequence_length, num_features) and return output 
	of the same shape. In this case, sequence_length is 288 and num_features is 1.

 • Detecting anomalies stage:
	 We will detect anomalies by determining how well our model can reconstruct the 
	input data.

 1. Find MAE loss on training samples.
 2. Find max MAE loss value. This is the worst our model has performed trying to reconstruct a 
sample. We will make this the threshold for anomaly detection.
 3. If the reconstruction loss for a sample is greater than this threshold value then we can infer 
that the model is seeing a pattern that it isn't familiar with. We will label this sample as an 
anomaly

### Review 
**What are the 4 time series prediction methods?**
- Classic Auto-regressive (AR) models 
- Bayesian AR Models
- General machine learning (feature extraction)
- Deep Learning 
**Systematic vs. Non-systematic Components?**
Systematic- structured changes like seasonality and trend 
Non-systematic - unstructured, cannot be modeled
**Cross-sectional vs. Longitudinal Analysis?**
Cross-sectional - look at many inputs and compare them between each other. 
Longitudinal - look at one input and compare it with itself across time. 
**Confounding, Explanatory, and Dependent Variables**
Confounding - hidden variables that, when not considered, can lead us to miscalculation or making incorrect assumptions about correlation. They are hidden, but affect the dependent variable and independent variables. 
Dependent variable - what we're trying to predict 
Explanatory variable - the data in input X that we are using to predict the dependent variable
**What is the advantage of ARIMA to AR and ARMA models?**
ARIMA can handle non-stationary data, whereas AR and ARMA models need stationary data. 
**Spurious Correlation**
When two variables move together but actually are not correlated at all. This might be some confounding variable affecting both. 
**How autocorrelation function (ACF) relates to auto-regressive model (AR)?**
ACFs measure how a time series relates to its own past values, which an AR is trying to model mathematically. 
**What deep architecture do we want to use for payment fraud and why?**
We would want to use an MLP, consisting of multiple dense layers to explore all of the features and Sigmoid activation to clamp between 0 and 1. 
**What deep architecture do we want to use for weather prediction and why?**
We would want to use an LSTM. This 
