# 297. Serialize and Deserialize Binary Tree

[297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

## Construct from 536 and 606

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        def traverse(root):
            if not root:
                return ''
            left = traverse(root.left)
            right = traverse(root.right)
            if len(left) == 0 and len(right) == 0:
                return str(root.val)
            elif len(left) == 0:
                return str(root.val) + '()' + '(' + right  +')'
            elif len(right) == 0:
                return str(root.val) + '(' + left  +')'
            return str(root.val) + '(' + left + ')' + '(' + right  +')'

        return traverse(root)

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        def traverse(s, begin):
            end = begin
            if begin == len(s):
                return None
            while end < len(s) and (s[end].isdigit() or s[end] == '-'):
                end += 1
            root = TreeNode(int(s[begin:end]))
            begin = end
            if end < len(s) and s[end] == '(':
                stack = []
                stack.append(s[end])
                end += 1
                while end < len(s) and stack:
                    if s[end] == '(':
                        stack.append(s[end])
                    if s[end] == ')':
                        stack.pop()
                    end += 1
                root.left = traverse(s[begin+1:end-1], 0)
            begin = end
            if end < len(s) and s[end] == '(':
                stack = []
                stack.append(s[end])
                end += 1
                while end < len(s) and stack:
                    if s[end] == '(':
                        stack.append(s[end])
                    if s[end] == ')':
                        stack.pop()
                    end += 1
                root.right = traverse(s[begin+1:end-1], 0)
            return root
        return traverse(data, 0)



# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

{% page-ref page="construct-binary-tree-from-string.md" %}

{% page-ref page="construct-string-from-binary-tree.md" %}

## Preorder

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        res = []
        def traverse(root):
            if not root:
                res.append('#')
                return
            res.append(str(root.val))
            traverse(root.left)
            traverse(root.right)
        traverse(root)
        return ','.join(res)

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if not data: return None
        nodes = data.split(',')
        def traverse(nodes):
            rootVal = nodes.pop(0)
            if rootVal == '#': return None
            root = TreeNode(rootVal)
            root.left = traverse(nodes)
            root.right = traverse(nodes)
            return root
        return traverse(nodes)



# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

## Postorder

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        res = []
        def traverse(root):
            if not root: 
                res.append('#')
                return
            traverse(root.left)
            traverse(root.right)
            res.append(str(root.val))
        traverse(root)
        return ','.join(res)



    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if not data: return None
        nodes = data.split(',')
        def traverse(nodes):
            rootVal = nodes.pop()
            if rootVal == '#': return None
            root = TreeNode(rootVal)
            root.right = traverse(nodes)
            root.left = traverse(nodes)
            return root

        return traverse(nodes)



# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

## Iteration \(BFS\)

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        res = []
        q = deque([root])
        while q:
            size = len(q)
            for i in range(size):
                node = q.popleft()
                if node:
                    res.append(str(node.val))
                    q.append(node.left)
                    q.append(node.right)
                else:
                    res.append('#')
        return ','.join(res)

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if not data: return None
        nodes = deque(data.split(','))
        rootVal = nodes.popleft()
        if rootVal == '#': return None
        root = TreeNode(int(rootVal))
        q = deque([root])

        while q:
            size = len(q)
            for i in range(size):
                node = q.popleft()
                leftVal = nodes.popleft()
                rightVal = nodes.popleft()
                if leftVal != '#':
                    node.left = TreeNode(int(leftVal))
                    q.append(node.left)
                if rightVal != '#':
                    node.right = TreeNode(int(rightVal))
                    q.append(node.right)
        return root



# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

