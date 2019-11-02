#121/122/123 Best time to buy/sell stocks

- 121 At most one transaction (which means we can choose not to complete any transaction if the prices are monotonically decreasing - we would buy a stock price and sell at a loss)
  - there are many ways to solve these problems. This problem also has two versions: the more common one is that we can at most make K transactions, but don't have to make any tranction, so our profit will never go beyond 0. But some requires us to make K transactions, which means we have to minimize losses as well (if stocks are monotoically decreasing, then we want to minimize the selling losses).
  - There are also different types of stocks. Some involve DP, some involve state recording. State recording means for each element, we treat it as a possibility for each of the state (buy/sell) to occur. 
    - State recording technique keeps track of the min stock price until the current element (which indicates we should buy at the current price), and max profit until the current element (if we sell at the current price with the min price until the current price). 
    - This takes advatange of the fact for a single price, it cannot be a buy price and sell price at the same time since we can at most do one transaction. 
    - We treat every single stock price as a potential selling price, and derive the profit for that day by subtracting the min stock price before that day. If there we do one transaction, then it must involve one of these days as a selling day, so we pick the max profit from all the potential selling days.
    
- 122 (complete as many transactions as possible)
  - Local valley/peak Greedy Solution. We want to divide each transaction as a non-overlapping continuous monotically increasing subarrays, we want to buy at the start of the subarray and sell at the end of the subarray. We use the next day's price to determine what to do for today, we either buy (when we do not have a stock and next day is higher), do nothing(because the next day is lower/higher than today's value), or sell(when we have a stock and next day is lower). 
  - If we use the local valley/peak, we can also determine the buying/selling days.
  - why selling/buy on the same day does not matter.
    - when we will buy the stock: because you'll know the future stock prices, you will never buy at today's price when the next day's price is lower. So if the stock prices are 3,1,5. You will not buy on 3, you will wait until 1. So we buy WHENEVER we know the next day's price is higher, and when to sell only comes into consideration after we buy, which means now we are on an ascending subarray.
    - Now, if know the stock prices are 1,3,5. and today is 3. Why sell today and gain 2(3-1), buy again at today's price (3), and sell tomorrow and gain 2 (5-3). You are making an extra transaction compared to just hold on to the stock today and sell tomorrow at 5 and making the same total profit( 5-1).
    - Thus, you never gain more profit by buying/selling on the same day. At best, you will make the same profit as if you held on to the stock and sell at a higher price. But you will make an extra meaningless transaction.

-  code
  ```cpp
  class Solution {
  public:
      int maxProfit(vector<int>& prices) {
          if (prices.size() <= 1) return 0;
          int i = 0, buy, sell, profit = 0, len = prices.size() - 1;
          while (i < len) { 
              while (i < len && prices[i + 1] <= prices[i]) //buy at the end of a decreasing array
                  i++;
              buy = prices[i];

              while (i < N && prices[i + 1] > prices[i]) //the index will start from the buying index, and sell at the end of the increasing array
                  i++;

              sell = prices[i];

              profit += sell - buy;
          }
          return profit;
      }
  };
  ```
    
    
    
