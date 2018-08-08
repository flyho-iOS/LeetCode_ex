## [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)

Given a list of daily temperatures, produce a list that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead. (给定一个list，index为日期，list[index]为当日温度，返回一个list为每日离下一个更暖的日子隔多少天)

For example, given the list temperatures = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].

```
class Solution:
    def dailyTemperatures(self, temperatures):
		
        ans = [0] * len(temperatures)
        stack = []
        for i , t in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < t:
                cur = stack.pop()
                ans[cur] = i-cur
            stack.append(i)
        
        return ans
```
