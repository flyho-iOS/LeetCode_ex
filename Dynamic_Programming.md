# 121. Best Time to Buy and Sell Stock

Say you have an array for which the ith element is the price of a given stock on day i.(给你一个数组prices，数组index代表第index天， prices[index]代表第index天的股价)

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.（如果你只允许最多交易一次【即买卖各一次】，设计一个算法计算最大利润）

Note that you cannot sell a stock before you buy one.（卖出股票前只能买入）

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
   n    	     2  7   9   3   1
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

## [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/description/)

On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.（给定一个数组，数组中都是非负整数，踩在一个梯级上就要花钱，可以一次走一步或者两步，计算到达尽头时最小的花费是多少）

###### Example 1:
* Input: cost = [10, 15, 20]  
* output: 15  
* Explanation: Cheapest is start on cost[1], pay that cost and go to the top.

```
例 cost = [2,7,9,3,1]
    n    	  start   2  7   9   3   1   end
  走(yes)	     	  0  0   2   7  10
  
```
###### 解题过程
```
     def minCostClimbingStairs(self, cost):
        dp0, dp1, dp2 = 0, 0, 0
        for i in range(2,len(cost)+1):
            dp0 = min(dp1+cost[i-1],dp2+cost[i-2])
            dp1, dp2 = dp0, dp1
        return dp0
```

## [646. Maximum Length of Pair Chain](https://leetcode.com/problems/maximum-length-of-pair-chain/description/)

You are given n pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair (c, d) can follow another pair (a, b) if and only if b < c. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

###### Example 1: 
	Input: [[1,2], [2,3], [3,4]]
	Output: 2
	Explanation: The longest chain is [1,2] -> [3,4]
	
###### 解题过程
```
O(nlogn)
class Solution:
    def findLongestChain(self, pairs):        
        cur, res = float('-inf'), 0
        # 遍历排序好的pairs
        for p in sorted(pairs, key=lambda x: x[1]):
            if cur < p[0]: 
                cur, res = p[1], res + 1
        return res
```

## [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/)

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

###### Example:

Input:
```
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
```

Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.

###### 解题过程
```
class Solution:
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m = len(grid[0])
        n = len(grid)
        dp = [[1 for _ in range(m)] for _ in range(n)]
        for i in range(n):
            for j in range(m):
            	   # 到达grid[0][0]只能是其本身
                if i == 0 and j == 0:
                    dp[i][j] = grid[i][j]
                elif i == 0: # 第一行的只能从左边到达，所以dp[i][j-1]
                    dp[i][j] = dp[i][j-1]+grid[i][j]
                elif j == 0: # 第一列只能从上面到达，所以取dp[i-1][j]
                    dp[i][j] = dp[i-1][j]+grid[i][j]
                else: # 剩余的情况，取上面或左边之间的最小值
                    dp[i][j] = min(dp[i-1][j],dp[i][j-1])+grid[i][j]
        return dp[-1][-1]
```