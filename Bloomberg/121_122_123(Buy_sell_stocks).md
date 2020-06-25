#121/122/123 Best time to buy/sell stocks

- 121 At most one transaction (which means we can choose not to complete any transaction if the prices are monotonically decreasing - we would buy a stock price and sell at a loss)
  - there are many ways to solve these problems. This problem also has two versions: the more common one is that we can at most make K transactions, but don't have to make any tranction, so our profit will never go beyond 0. But some requires us to make K transactions, which means we have to minimize losses as well (if stocks are monotoically decreasing, then we want to minimize the selling losses).
  - There are also different types of stocks. Some involve DP(state recording), some involve greedy. 
    - Greedy solution stores the min stock price until the current day(means we should update the min price and save it for potential future sales) and max profit until the current day (current profit = the current price - the min price stored). 
    - This takes advatange of the fact for a single price, it cannot be a buy price and sell price at the same time since we can at most do one transaction. So we treat every single stock price as a potential selling price, and derive the profit for that day by subtracting the min stock price before that day. If there we do one transaction, then it must involve one of these days as a selling day, so we pick the max profit from all the potential selling days.
    
- 122 (complete as many transactions as possible)
  - Local valley/peak Greedy Solution. We want to identify each transaction as a non-overlapping continuous monotonically increasing subarrays, we want to buy at the start of the subarray and sell at the end of the subarray. We use the next day's price to determine what to do for today, we either buy (when we do not have a stock and next day is higher), do nothing(because the next day is lower/higher than today's value and we already have a stock), or sell(when we have a stock and next day is lower). 
  - If we use the local valley/peak, we can also determine the buying/selling days.

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
 - 123 Complete at most 2 transactions
  - This problem requires DP and it is thoroughly analyzed on handwritten notes/Ipad.
  
