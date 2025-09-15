**1) Missing Data**
Consider a dataset that has NULL values or missing cells. We have some options:
- Eliminate the row containing the missing data:
	- Can work for few occurrences of missing data
	- Can bias the data by obscuring the reason why there is missing data
- Place a threshold on certain columns/features that decide whether or not to eliminate the feature altogether if the percentage of missing data passes that threshold. 
- *Imputation* - take those columns where we having a NULL value and replace it with some value. How we do this depends on the data. 
	- Numerical data: use average or median value. 
	- Alphanumeric data: 