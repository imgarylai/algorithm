# 572. Subtree of Another Tree

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    
    def isMatch(self, TreeA: TreeNode, TreeB: TreeNode):
        if not TreeA or not TreeB:
            return TreeA == TreeB
        return (TreeA.val == TreeB.val and self.isMatch(TreeA.left, TreeB.left) and self.isMatch(TreeA.right, TreeB.right))
    
    def isSubtree(self, root: TreeNode, subRoot: TreeNode) -> bool:
        if self.isMatch(root, subRoot):
            return True
        if not root:
            return False

        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
```

