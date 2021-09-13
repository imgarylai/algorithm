# 230. Kth Smallest Element in a BST

[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

## 中序遍歷

中序遍歷的順序，就是 BST 的大小順序

```python
class Solution:
    def __init__(self):
        self.rank = 0
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:

        ans = root.val
        def inorder(root):
            nonlocal ans
            if not root:
                return
            inorder(root.left)
            self.rank += 1
            if self.rank == k:
                ans = root.val
            inorder(root.right)

        inorder(root)
        return ans
```

## 迭代（中序遍歷）

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        while True:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            k -= 1
            if not k:
                return root.val
            root = root.right
```

