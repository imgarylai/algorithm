# 701. Insert into a Binary Search Tree

[701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

如果是要在一個 BST 中插入一個點，那我們要做的就是先找到是哪個點可以插入，一樣用二分搜索的方式，先找到哪裡需要插入，是要插入在左子樹，還是插入在右子樹。

最後的 Base case 是當走到最後時，透過題目給個目標值建立一個新的節點並回傳。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return TreeNode(val)
        if root.val > val:
            root.left = self.insertIntoBST(root.left, val)
        elif root.val < val:
            root.right self.insertIntoBST(root.right, val)
        return root
```

