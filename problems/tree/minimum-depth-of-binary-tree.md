# 111. Minimum Depth of Binary Tree

[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        queue = deque([root])
        level = 0
        
        while queue:
            size = len(queue)
            level += 1
            for i in range(size):
                node = queue.popleft()
                if not node.left and not node.right:
                    return level
                else:
                    if node.left:
                        queue.append(node.left)
                    if node.right:
                        queue.append(node.right)
        return level
```

