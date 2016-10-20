Title: 104. Maximum Depth of Binary Tree
Date: 2016-06-24 10:30:53
Category: LeetCode
Tags:
Slug: 104_Maximum_Depth_of_Binary_Tree
Author: Lemon Tree

## Question

    Given a binary tree, find its maximum depth.
    The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Solution

  因为给的是二叉树，所以直接利用递归依次遍历两个子节点来计算深度就好。第一次做这样的题，如果不看讨论区里的答案，还真不知道怎么去写。

### Show me the code

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right)) if root else 0
```

\- 完 -
