# 121. Best Time to Buy and Sell Stock

    Say you have an array for which the ith element is the price of a given stock on day i.
    (给你一个数组prices，数组index代表第index天， prices[index]代表第index天的股价)
    If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.
    （如果你只允许最多交易一次【即买卖各一次】，设计一个算法计算最大利润）
    Note that you cannot sell a stock before you buy one.
    （卖出股票前只能买入）

###### Example 1:

    Input: [7,1,5,3,6,4]
    Output: 5
    Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
             
###### Example 2:
    Input: [7,6,4,3,1]
    Output: 0
    Explanation: In this case, no transaction is done, i.e. max profit = 0.

```
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_profit, min_price = 0, float('inf')
        for price in prices:
            min_price = min(min_price, price)
            profit = price - min_price
            max_profit = max(max_profit, profit)
        return max_profit
```
