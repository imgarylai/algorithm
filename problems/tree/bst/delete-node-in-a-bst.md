# 450. Delete Node in a BST

[450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:
        if not root: return root
        if root.val > key:
            root.left = self.deleteNode(root.left, key)
        elif root.val < key:
            root.right = self.deleteNode(root.right, key)
        elif root.val == key:
            if not root.left:
                return root.right
            elif not root.right:
                return root.left
            smallestOnRight = root.right
            while smallestOnRight.left:
                smallestOnRight = smallestOnRight.left
            root.val = smallestOnRight.val
            root.right = self.deleteNode(root.right, smallestOnRight.val)
        return root
```

