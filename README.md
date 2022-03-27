# Aspen Algorithm

## DEMO:
[![Watch the video](https://s29755.pcdn.co/wp-content/uploads/2019/07/FWLIVE_CHI_Web-05.png)](https://youtu.be/Ka_fOdJNVL8)


## Description
This is a 3-person project. The goal of this project is to generate the riskiest portfolio with a minimum of 10 stocks and a maximum of 20 stocks with any given ticker set and initial investment. 

## Strategy/Algorithm:

We analyzed each stock's history in the time between July 2nd and November 26th of 2021. The starting date was chosen to be July 2nd because we are interested in the short term volatility of the stocks as the portfolios are only tracked for a week for the competition. Thus, we needed a timeframe short enought to capture current information about the stocks (ie. maybe there is some bad press/new legislation that disturbed the stock price recently but the stock is normally quite stable - we are still interested in this stock since the portfolio is only tracked for a week) but long enough to contain sufficient information for a proer analysis. We thought that July 2nd, which was also the timeframe we started tracking the volume of the stocks, was a healthy medium that fulfilled our needs. November 26th is a much more self-explanatory choice: we want to get the latest data prior to generating the portfolio.

In our analysis of each stock, we chose to find the most volatile stock by finding the stock with the highest standard deviation, meaning that the stock will be more likely to move further away from its average rate of returns. This brings our portfolio the most possible individual risk a stock in the list can bring, which sets a foundation for our "riskiest portfolio".

Since we want the riskiest portfolio possible, then we want to preserve the risk of the riskiest stock as much as possible since the addition of any "non-1" correlated stock (which is every stock other than itself) will always diversified away some (may be very small or large) risk from the portfolio. Therefore, we will only choose 10 stocks (the minimum required) to form our portfolio so the riskiest stock's risk will be prioritized and preserved. In choosing the other 9 stocks, we decided to find the stocks that had the highest correlation with the riskiest stock since those stocks will most resemble the shape of the riskiest stock and thus preserve the risk of the riskiest stock. 

As mentioned before, our strategy depends on maximizing the singular risk of the riskiest stock and minimizing the effect of diversification from any other stock that is added to the portfolio since we believe that will produce the highest risk possible for our portfolio. Then naturally, we will weigh the stocks in a way that follows that principle, so our weighing is as follows. We will use 35% (the maximum for a single stock) of our portfolio on purchasing the riskiest stock, 25% (the maximum while allowing the rest of the stocks to have an minimum amount invested) on purchasing the stock that correlated the highest with the riskiest stock, and 5% on each of the other stocks. This allows us to maximize the risk of the portfolio by preserving the risk of riskiest stock (since the stock that is most correlated to the riskiest will preserve that risk the best) and minimizing the impact of diversification from the other stocks on our portfolio.

Notice in the algorithm discuss above that there is a chance of failure of that algorithm: if the stock with the highest standard deviation is poorly correlated with all of the other stocks, then there might exist another stock that still has a very high standard deviation and also is highly correlated with many other stocks, which can form a portfolio of 10 stocks that might beat the portfolio generated from the original algorithm in terms of risk. This is because a low correlation with the rest of the stocks in a portfolio can result in heavy diversification of risk, which, in turn, heavily lowers the standard deviation of the portfolio.

Our solution to this is to test all of the possible portfolios that could potentially beat the first one we generated. However, doing that could require a lot of computing resources and time, so we did it in a way that eliminates the need to go through every single possibility.

Since we know that the maximum standard deviation of a portfolio is the standard deviation of the riskiest stock in that portfolio and our previous algorithm involves finding a stock that has a high standard deviation and building a portfolio around that stock, then we can safely assume that any stock with a standard deviation lower than the standard deviation of the first portfolio we found cannot be used to generate a portfolio with a higher standard deviation. Also, note that the case of having a higher standard deviation stock in the 9 correlated stocks which could bring the standard deviation of newly generated portfolio higher than the stock it is built around is handled in the recursion: any stock that has a higher standard deviation and a high correlation with this stock is already considered before this stock.
