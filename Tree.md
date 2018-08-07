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

## [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).(给定一棵二叉树，返回一个按层级顺序存储的结果)

For example:
Given binary tree [3,9,20,null,null,15,7],

return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]

#### 解题过程

```
class Solution:
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        # 根节点为空，返回[]
        if not root:
            return []
        
        res = [[root.val]]
        # 从左往右进行递归，深度从1开始
        self.helper(root.left,1,res)
        self.helper(root.right,1,res)
        return res
        
    # param depth 可看做res的index
    def helper(self,node,depth,res):
    	 # 当节点为空，则return 
        if not node:
            return
        # 如果当前深度的list已存在，直接append    
        if depth < len(res):
            res[depth].append(node.val)
        # 如果不存在，则创建
        else:
            res.append([node.val])
        # 再往下递归，因此深度+1
        depth += 1
        self.helper(node.left,depth,res)
        self.helper(node.right,depth,res)
```