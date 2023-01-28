# 224. Basic Calculator

[224. Basic Calculator](https://leetcode.com/problems/basic-calculator/)

{% hint style="info" %}
先做 [227. Basic Calculator II](227.-basic-calculator-ii.md) 和 [394. Decode String](../../problems/stack/394.-decode-string.md)
{% endhint %}

```python
class Solution:
    def calculate(self, s: str) -> int:
        def helper(s):
            num = 0
            stack = []
            sign = '+'
            while s:
                c = s.popleft()
                if c.isdigit():
                    num = 10 * num + int(c)
                if c == '(':
                    num = helper(s)
                if not c.isdigit() and not c.isspace() or len(s) == 0:
                    if sign == '+':
                        stack.append(num)
                    elif sign == '-':
                        stack.append(-num)
                    elif sign == '*':
                        stack.append(stack.pop() * num)
                    elif sign == '/':
                        stack.append(int(stack.pop() / num))
                    sign = c
                    num = 0
                if c == ')': break
            return sum(stack)
        return helper(deque(list(s)))
```
