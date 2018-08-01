# 121. Best Time to Buy and Sell Stock

    Say you have an array for which the ith element is the price of a given stock on day i.
    (给你一个数组prices，数组index代表第index天， prices[index]代表第index天的股价)
    If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.
    （如果你只允许最多交易一次【即买卖各一次】，设计一个算法计算最大利润）
    Note that you cannot sell a stock before you buy one.
    （卖出股票前只能买入）

#### 解题
```
class Solution(object):
    def maxProfit(self, prices):
        ## 声明两个变量，记录最大利润max_profit、最小成本min_price
        max_profit, min_price = 0, float('inf')
        for price in prices:
            ## 遍历数组，记录最小成本
            min_price = min(min_price, price)
            ## 计算某天卖出的利润
            profit = price - min_price
            ## 计算记录某天卖出的利润是否最大
            max_profit = max(max_profit, profit)
        return max_profit
```

## [198. House Robber](https://leetcode.com/problems/house-robber/description/)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night. (简单讲就是相邻的房子不能抢)

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

```
  例 [2,7,9,3,1]
	 n    		 2  7   9   3   1
  抢(yes)	     2  7  11  10  12
  不抢(no)	     0  2   7  11  10
  
  由以上规律可得，yes = no + n,  no = max(yes,no)

```

```
	def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:return 0
        
        yes, no = 0, 0
        for n in nums:
            no, yes = max(yes,no), n + no
        return max(yes,no)
```