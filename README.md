# OptyX
As of 7/5 SpyDataRawV4 has inflation + Sentiment 

______________________________

Disclaimer:

Within the OptyX repo - you will notice numerous versions of notebooks & csv files - These remain to demonstrate that there were multiple iterations of code restructuring and data formatting that took place before our final versions.

Data Gathering: 

The data gathering process for both VIX & SPY option contracts data i.e. (Strike Price, SPY Price, Greeks, Expiration, Call Last Price etc.) was directly pulled from optionsdx.com website - This website provides a suite of historical options data. 

We decided to look at 6 months worth of historical data from October 2021 (Q4) to March 2022 (Q1) 

The data was downloaded in the form of text files, with each month of data being a separate txt file. We then had to convert them into DataFrames before further filtering them. Once the data was formatted accordingly we were able to save it as individual csv files and concatenate them into one large dataset. 

Some insight into the data & filtering process:

	- The option data was in 30 minute increments
	- There were a total of over 9 million rows (before data cleaning) 
	- Post data cleaning and filtering, we were left with about 35k rows.
	- We filtered the Strike Prices within 3% of the Underlying asset price (SPY)
	- We filtered the Expiration Date to Weekly contracts (Expiring the same week, Mon-Fri)
	- We held onto the contract for 3 days, until Wed @ Close - This was done to monitor the max effect & change in the Greeks. Wanted to see if that produced any insights into the value of the option contract. 
	- Recalculated the Strike Distance formula to showcase negative values (for ITM contracts) (Made easier to filter)

	Introduced some features 
	- Inflation data (MoM increase - duplicated over a month to populate all rows
	- ROI % of a contract
	- Defined categories for our Target Variable (y)

	0 = Strong Sell		| (< - 60%)
	1 = Sell 		| (> -60% to < -10%)
	2 = Pass		| (> -10% to 10%)
	3 = Buy 		| (> 10% to < 60%)
	4 = Strong Buy  	| (> 60% to < 80%)| 
	5 = Very High Return    | (> 100%)



After we combined SPY, VIX, Inflation, Sentiment data we then ran it in our into ML Model. 

_________________________________

Part 2: Binomial Option Pricing Tree 

The code in this folder is an example of what the Binomial Model which will be deployed in our later development. 
Our machine learninng process produces unique probabilities to each target outcome. 
By using these probabilities we will understand the R/R of the contract at each upward/downward move in the underlying. 
Using this model will allow the user to understand how the contract prices behave, and when R/R values change to a point where some exposure needs to be reduced/ added to support the strategy. 
