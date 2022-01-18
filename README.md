# Quantitative Analysis Performance of Top Hedge Funds Against the S&P 500

## This project is broken down into 4 categories:
* Analyze the Performance
* Analyze the Volatility
* Analyze the Risk
* Analyze the Risk-Return Profile
* Diversify the Portfolio

## Analyze the Performance:
* To analyze thre data we first had to import the CSV file data:

* After reading and plotting the first 5 rows of the CSV file, we used the `pct_change` and `.dropna()` functions to find the daily returns for the funds

`whale_daily_returns = whale_portfolio_df.pct_change().dropna()`

`whale_daily_returns.head()`

* Next, we created a function that visulaized the daily return data for the four funds and S&P 500:

`whale_daily_returns.plot(figsize=(15,10), title="Whale Portfolio with S&P 500 Daily Returns 2015-2021")`
* We then used the `cumprod` and function to find the cumulative returns for the four funds:
`whale_cumulative_returns = (1 + whale_daily_returns).cumprod()`
* After finding the cumulative returns we plotted the returns on a graph over time:  The S&P had the greatest gains followed by Berkshire, Tiger Global, Soros fund, and lastly Paulson and Co. 
---
## Analyze the Volatility:
* We started analyzing volatility by plotting the funds daily returns alongside the S&P on a box plot to visually see the spread.
`whale_daily_returns.plot(figsize=(15,10), kind='box', title='Whale Portfolio with S&P 500 Daily Return Spread')`

* After creating a box plot with the S&P we decided to create one without it to take a closer look at the spread of the four funds.

We were able to do this by using the  `.drop` function to get rid of the S&P column from the Dataframe and renamed the new Dataframe as:  `solo_whale_daily_returns`

---
## Analyze the Risk:
* To analyze the risk of the funds we first took the standard deviation of the funds daily return data to take a closer look at the spread.  
`whale_daily_returns.std().sort_values()`
* After calculating the standard deviation, we calculated the annual standard deviation to by using the following code:
`trading_days= 252`

`annual_standard_deviation= whale_daily_returns.std() * np.sqrt(trading_days)`

`annual_standard_deviation.sort_values()`
* Next, we plotted the rolling 21-day standard deviation for the four funds and S&P 500 and then another plot with just the four funds: 
`whale_daily_returns.rolling(window=21).std().plot(figsize=(15,10), title='Rolling 21-day Standard Deviation of Whale Portfolios with S&P Daily Returns')`

---
## Analyze the Risk-Return Profile
* First we calculated the annual average return data by using the `.mean()` function for our daily return values and mulitiplied that by the number of trading days.
* After finding the annual average return data we were able to calculate the Sharpe ratio by dividing annual average return data by the annual standard deviation data: 
`whale_sharpe_ratios = annual_average_whale_portfolio / annual_standard_deviation`
* Once the Sharpe ratios were calculated they were plotted on a bar chart to visually compare the values amongst the four funds. We found that Berkshire Hathaway had the best risk-return profile since it had the highest Sharpe ratio

---
## Diversify the Portfolio:
* We decided to take a closer look at two funds we believed to be the most profitable, Tiger Global and Berkshire Hathaway funds:

* We started by calculating the covariance of the S&P 500, Tiger Global and Berkshire Hathaway funds using a 60-day moving average.
:
`cov_HATHAWAY_portfolio = whale_daily_returns['SOROS FUND MANAGEMENT LLC'].rolling(window=60).cov(whale_daily_returns['S&P 500'].rolling(window=60))`
* After calculating these 3 values we divided Tiger Global's and Berkshire Hathaway's 60 day-rolling covariance by the S&P's 60 day-rolling covariance to calculate their respective Beta values:
`BETA_Hathaway= cov_Hathaway_portfolio / var_SP_500`
* To find their actual Beta values, we had to take the mean from the results:
`BETA_Hathaway.mean()`
* After finding the mean of the Beta values, we plotted the results of all the beta values from 2016-2021:
`BETA_Hathaway.plot(figsize= (15,10), title= 'Berkshire Hathaway INC 60-day Rolling Beta')`




