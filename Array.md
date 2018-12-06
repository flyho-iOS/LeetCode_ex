## [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).

Find the minimum element.

You may assume no duplicate exists in the array.

Example 1:

Input: [3,4,5,1,2] </br>
Output: 1
Example 2:

Input: [4,5,6,7,0,1,2]</br>
Output: 0

###### 解题思路
```
class Solution(object):
    def findMin(self, nums):

        i, j = 0, len(nums) - 1
        while i < j:
            m = i + (j - i) / 2
            if nums[m] > nums[j]:
                i = m + 1
            else:
                j = m
        return nums[i]
```

##[442. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/)

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

###### Example:
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]

###### 解题思路
```
class Solution:
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = []
        for x in nums:
        	## 遍历到的数值n-1作为index，如果小于0，表示在之前遍历过的数中已经出现过
            if nums[abs(x)-1] < 0:
                res.append(abs(x))
            else: ## 如果大于0，即未出现过，取相反数，表示已经出现过了
                nums[abs(x)-1] *= -1
        return res
```