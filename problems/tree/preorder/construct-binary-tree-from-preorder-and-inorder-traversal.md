# 105. Construct Binary Tree from Preorder and Inorder Traversal

[105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

這一題的重點是，Preorder 的造訪順序是根節點 -&gt;  左子樹 -&gt; 右子樹

preorder 的順序，就是根節點是第一個數字

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        table = {}
        for idx, val in enumerate(inorder):
            table[val] = idx
        
        preorder = deque(preorder)

        def traverse(leftIndex, rightIndex):
            if leftIndex > rightIndex:
                return None
            root = TreeNode(preorder.popleft())
            rootIndex = table[root.val]
            root.left = traverse(leftIndex, rootIndex - 1)
            root.right = traverse(rootIndex + 1, rightIndex)
            return root
        return traverse(0, len(inorder) - 1)
```

