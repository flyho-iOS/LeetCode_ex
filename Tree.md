## [100. Same Tree](https://leetcode.com/problems/same-tree/description/)

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

#### Example 1:
``` 
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```
#### 解题过程
```
class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        queue = []
        queue.append((p,q))
        while queue:
            n1, n2 = queue.pop()
            if not n1 and not n2:
                continue
            if not n1 or not n2:
                return False
            if n1.val != n2.val:
                return False
            queue.append((n1.left,n2.left))
            queue.append((n1.right,n2.right))
        return True
```