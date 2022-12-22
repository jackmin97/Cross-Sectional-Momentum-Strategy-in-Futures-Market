# Cross-Sectional-Momentum-Strategy-in-Futures-Market
In this strategy, we take position on a large number of futures picked out from a future commodity universe.
Commodity momentum returns are found to be related to the propensity of commodity futures markets to be in backwardation or contango. A momentum strategy that consistently trades the most backwarded and contangoed contracts is likely to be profitable. Therefore, we can use the configuration of the term structure or forward curve as a proxy for the momentum which a futures contract might have.

### 1. Import modules
First, we will import the necessary libraries.

### 2. Read prices from CSV file
We will import the commodity future and spot data. The data is from the beginning of 2012 to the end of 2019.

### 3. Rank based on future spot ratio
We will calculate:

1. The futures-spot ratio: this gives a sense of how backwarded or contangoed a contract is. The higher the ratio more contangoed it is as the futures price is higher relative to spot. Similarly, the lower the value more backwarded it is.

2. The rank based on the ratio. The more contangoed the commodity future spot pair is the higher the rank. Backwarded commodities have a lower rank.

In a few places the ranks have a fractional component. This is the average rank of the group of assets which are tied at the same rank.

Since the future spot ratio of natural gas is the highest it has the highest rank. It is the lowest for wheat so it has the lowest rank.

### 4. Plot future spot ratio
We plot the future-spot ratio. The ratio will spike when the contract is either extremely contangoed or backwarded.

### 5. Commodity spot correlation
We plot the correlation between an equally weighted portfolio of commodity spots and spot of each commodity. As we can observe majority of the commodity spots have a correlation magnitude less than 0.5.

### 6. Generate the trading signal
We generate the trading signal based on the rank. We will be taking the commodities of the two upper and two lower deciles for trading. This can be done by decile ratio below being multiplied to the variable total_ranks.

We go short on contracts with the future spot ratio in the bottom two deciles. We simultaneously go long on all contracts who’s future spot ratio is in the top two deciles.

### 7. Calculate returns
We set the holding period. The holding period is the number of days where we hold our position. After the holding period, we rank the commodities again and take positions.

Thereafter, we calculate the returns based on the generated signals.

### 8. Calculate trading cost
We calculate the trading cost. The cost gets applied only when the position changes between consecutive trading days. Like for example if the signal goes from 0 (no position) to -1 (sell), the cost for selling will be applied. If the position changes no cost will be applied.

### 9. Evaluate the strategy
We evaluate the strategy by calculating the cumulative returns, the drawdowns and the sharpe ratio.

The maximum drawdown is between 2016 and 2017. This is because of the increase in the spot price for a lot of commodities simultaneously in mid-2016. When they increase simultaneously, there is a net spot movement. We expected this net movement to be 0 but it didn't happen. 

Conclusion
The backtest gave us a Sharpe of 1.74 and a return of 522% over a period from the beginnin of 2012 to the beginning of 2020. The maximum drawdown is -22.5%.
