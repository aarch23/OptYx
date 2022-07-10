# OptyX
As of 7/5 SpyDataRawV4 has inflation + Sentiment 


______________________________

Start: 

Within the OptyX repo - you will see numerous versions of notebooks & csv files - These have been left to show that there were multiple iterations of code restructuring and data formatting that took place before our final versions.

Data Gathering: 

The  data gathering process for both VIX (prices) & SPY (option contracts data) i.e. (Strike Price, SPY Price, Greeks, Expiration, Call Last Price etc.) was directly pulled from optionsdx.com website - This website provides a suite of historical options data. 

We decided to look at 6 months worth of historical data from October 2021 (Q4) to March 2022 (Q1) 

The data was downloaded in the form of text files, with each month of data being a separate txt file. We then had to import/convert them into DataFrames before filtering them to our desired choice? , before then exporting them into their individual csv's & concatting/combining them into one large dataset. 

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


0 = Strong Sell
1 = Sell
2 = Pass
3 = Buy
4 = Strong Buy
5 = Very High Return 

0 is (< - 60%)
1 is (> -60% to < -10%)
2 is (> -10% to 10%)
3 is (> 10% to < 60%)
4 is (> 60% to < 80%)
5 is (> 100%)
  

Combined SPY, VIX, Inflation, Sentiment data --> then fed into ML Model. 

_________________________________

Part 2: Binomial Option Pricing Tree 

The code in this folder is an example of what the Binomial Model will be utilized for next: To understand the different probabilities assigned to a upward and downward move in the price of SPY. Using this, we hope/will be able to get a better understanding of our Risk at each time step (Day 1, 2, 3) - and will be able to see our Expected Value and evaluate Risk accordingly. This will serve as a "blueprint/guide???"  to knowing when to potentially take profit/exit a trade. ![image](https://user-images.githubusercontent.com/100783805/178165157-b53b29b8-444e-4c08-939a-5df594b8a7b8.png)
