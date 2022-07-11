<img src= "images/optyx.png" width="930" height="300">
# __OptyX: Overview__
The proprietary OptyX technology implements machine learning as a means of predicting the percent profit or loss of a weekly call option's contract at two days until expiration using various option contract variables (present call option price, strike price, underlying asset price, the Greeks, implied volatility, and volume), along with VIX prices, inflation percent, and various sentiment metrics. The predicted profit or loss, the 'y' outcome, is classified into the following three classes: ['0'] a loss of a contract's value greater than 30%, which constitutes a "Sell to Open" recommendation, ['1'] a change in a contract's value between -30% and 25%, which constitutes a "Pass" recommendation, and finally ['2'] a gain in a contract's value greater than 25%, which constitutes a "Buy to Open" recommendation.
This section of the OptyX repo serves as a blueprint for navigating the OptyX repo. The following instructions will guide the user through the process of installing necessary libraries and running the applicable Jupyter notebooks, as well as provide a step-by-step explanation of the code's usage. 
---
## __Technologies__
This application leverages Python 3.7. 
---
## __Installation Guide__
Begin by cloning the GitHub repo (the same repo that this README.md file is contained within) into your terminal. 
Then activate the correct environment by inputting the following command into your terminal:
`conda activate dev`
Within this environment, next install the above listed dependencies. To do so, in your terminal while in this same repo, enter `pip install -r requirements.txt`.
---
## __Disclaimer__
Within the OptyX repo, you will notice numerous versions of notebooks & csv files - These remain to demonstrate that there were multiple iterations of code restructuring and data formatting that took place before our final versions.
---
## __Data Gathering__ 
Please see **SPY_21Q4_22Q1_V3.ipynb** (contained within the same folder that this README.md file is contained in).
The data gathering process for both VIX & SPY option contracts data i.e. (Strike Price, SPY Price, Greeks, Expiration, Call Last Price etc.) was directly pulled from optionsdx.com website - This website provides a suite of historical options data. 
Our data covers a 6 months period from October 2021 (Q4) to March 2022 (Q1) 
The data was downloaded in the form of text files, with each month of data being a separate txt file. We then had to convert them into DataFrames before further filtering them. Once the data was formatted accordingly we were able to save it as individual csv files and concatenate them into one large dataset. 
Some insight into the data & filtering process:
    - The option data was in 30 minute increments
    - There were a total of over 9 million rows before data cleaning. 
    - Post data cleaning and filtering, we were left with about 35k rows.
    - For the purpose of our model, our focus was just on Call contracts, where we can classify 3 trade scenario per 1 type of move of the underlying, where the        inclusion of puts would add another near inverse dimension.
    - We filtered the strikes within -3+15 of (SPY) price to accumudate larger moves.
    - We filtered the Expiration Date to Weekly contracts (Expiring the same week, Mon-Fri)
    - We defined the max hold period at 2.0DTE (Wednesday close). This was done so we could study the rapid change of greeks and their effect on the contract.
    - Recalculated the Strike Distance formula to showcase negative values for ITM contracts.
    We then introduced a few unique features: 
    - Inflation data (MoM increase - duplicated over a month to populate all rows
    - ROI % of a contract, to be able to assign our outcome ranges.
    - Defined categories for our Target Variable (y)
    - Combined SPY, VIX, Inflation, and Sentiment data.
**Features Introduced:**
    
- Inflation data (MoM increase - duplicated over a month to populate all rows
- ROI % of a contract
- Defined categories for our Target Variable (y) according to the following criteria:['0'] a loss of a contract's value greater than 30%, which constitutes a "Sell to Open" recommendation;
['1'] a change in a contract's value between -30% and 25%, which constitutes a "Pass" recommendation; and ['2'] a gain in a contract's value greater than 25%, which constitutes a "Buy to Open" recommendation.

---
## __PART 1: Machine Learning__
Please consult the README.md within folder **'Part1'** for the machine learning aspect of the OptyX product. Provided instructions detailed in this README.md will guide the user through navigating and comprehending the machine learning aspect of OptyX technology.
---
## __PART 2: Binomial Option Pricing Trees__
The code in this folder is an example of what the Binomial Model which will be deployed in our later development. 
Our machine learninng process produces unique probabilities to each target outcome. 
By using these probabilities we will understand the R/R of the contract at each upward/downward move in the underlying. 
Using this model will allow the user to understand how the contract prices behave, and when R/R values change to a point where some exposure needs to be reduced/ added to support the strategy. 
---
## __Contributors__
Bar, Kfir
Malhotra, Aarchit
Naqvi, Aliza
Roberts, Nicole
Rosa, Wilson








BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB_______________________

# __OptyX: Machine Learning__

---

Disclaimer:

Within the OptyX repository, you will notice numerous versions of different Jupyter notebooks & csv files - These remain to demonstrate that there were multiple iterations of code restructuring and data formatting that took place before our final versions.

---

# __OptyX: Data Gathering__ 

The data gathering process for both VIX & SPY option contracts data i.e. (Strike Price, SPY Price, Greeks, Expiration, Call Last Price etc.) was directly pulled from optionsdx.com website - This website provides a suite of historical options data. 

Our data covers a 6 months period from October 2021 (Q4) to March 2022 (Q1) 

The data was downloaded in the form of text files, with each month of data being a separate txt file. We then had to convert them into DataFrames before further filtering them. Once the data was formatted accordingly we were able to save it as individual csv files and concatenate them into one large dataset. 

Some insight into the data & filtering process:

	- The option data was in 30 minute increments
	- There were a total of over 9 million rows before data cleaning. 
	- Post data cleaning and filtering, we were left with about 35k rows.
	- For the purpose of our model, our focus was just on Call contracts, where we can classify 3 trade scenario per 1 type of move of the underlying, where the 		inclusion of puts would add another near inverse dimension.
	- We filtered the strikes within -3+15 of (SPY) price to accumudate larger moves.
	- We filtered the Expiration Date to Weekly contracts (Expiring the same week, Mon-Fri)
	- We defined the max hold period at 2.0DTE (Wednesday close). This was done so we could study the rapid change of greeks and their effect on the contract.
	- Recalculated the Strike Distance formula to showcase negative values for ITM contracts.

	We then introduced a few unique features: 
	- Inflation data (MoM increase - duplicated over a month to populate all rows
	- ROI % of a contract, to be able to assign our outcome ranges.
	- Defined categories for our Target Variable (y)

		0 = Strong Sell		| (< - 60%)
		1 = Sell 		| (> -60% to < -10%)
		2 = Pass		| (> -10% to 10%)
		3 = Buy 		| (> 10% to < 60%)
		4 = Strong Buy  	| (> 60% to < 80%)| 
		5 = Very High Return    | (> 100%)


After we combined SPY, VIX, Inflation, Sentiment data we then ran it in our into ML Model. 

---

## __PART 1: Machine Learning__

Please consult the README.md within folder **'Part1'** for the machine learning aspect of the OptyX product. Provided instructions detailed in this README.md will guide the user through navigating and comprehending the machine learning aspect of OptyX technology.

## __PART 1: Binomial Pricing Model__

Please consult the README.md within folder **'Part2'** to understand the next steps for this project. 

---

Contributors: 

Bar, Kfir
Malhotra, Aarchit
Naqvi, Aliza
Roberts, Nicole
Rosa, Wilson
