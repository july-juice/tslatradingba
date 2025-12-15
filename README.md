# Trading Business Analysis - TSLA

In this project, the pandas library is used for data handling. Historical stock prices are taken from the yfinance (Yahoo Finance) library as well as downloading real market data and company financials like revenue and net income. The matplotlib library is used for charting and plotting this real-time data.

Analysed in this project are 2 years of Tesla (TSLA) stock prices. In a dataframe, Tesla's income statement (revenue, cost of revenue, gross profit and net income) is returned as a pandas DataFrame, with the columns as years and the rows being the financial metrics. 2 years of daily data are downloaded in another pandas DataFrame, which was subsequently utilised for calculating returns, adding indicators (SMA, RSI, MACD), generating trading signals, and backtesting strategies.

Revenue and net income are pulled from the financial statements of Tesla and organised into a clean table, for the calculation of revenue growth over time and the growth in profit margin. A visual inspection of this business_df is added for a sanity check.

The inherent issue with the prices DataFrame is that it had MultiIndex columns (e.g., ('Close', 'TSLA')), so these were flattened into single-level strings.

To ensure trading decisions are rule-based and comparable, three different trading strategies are built over Tesla's historical share price data:

### Trend-following - SMA(20)
- A 20 day moving average is applied to smooth over the price
- Shares are bought when the prices is above the average and sold when it drops down below
- Attempts to avoid downward trends and follow upward trends

### Momentum/overbought - RSI
- RSI measures whether stock is potentially oversold or overbought.
- Shares are bought when the price appears oversold (RSI < 30) and sold when overbought (RSI > 70).

### Momentum crossover - MACD
- Compares short and long-term momentum
- Buy when short-term momentum overtakes long term. Sell when that momentum weakens.

Clear buy/sell signals are then created.

All three strategies are then compared alongside each other and the buy-hold share price, converting the trading signals into daily strategy returns. These results are compounded to show the growth of an inital investment. The code is also future-cheat proof as signals are shifted by 1, ensuring decisions are made after the signal.

The plots include Tesla's business performance, TSLA stock price vs its 20-day moving average, and the strategies vs buy-hold performance.

# Strategy Evaluation

When observing the buy-and-hold performance, TSLA's 92% percent 2 year stock growth shows a strong baseline and reflects Tesla's upward price movement. The SMA crossover strategy resulted in 61 total trades and resulted in a 51% increase in stock value. While the strategy captured some upward trends, frequent trends caused it to miss parts of longer rallies, leading to underperformance compared to buy-and-hold.

The RSI strategy is inherently determined on short-term mean-reversion signals. The value of an initial $1 investment essentially broke even, suggesting a lack of effectiveness in a generally trending market. By far the best performer was the MACD strategy, growing $1 to $2.02, slightly outperforming buy-and-hold. MACD's trend-following nature allowed it to stay invested during sustained price movements while filtering out some market noise.
