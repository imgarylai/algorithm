# 227. Basic Calculator II

[227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/)

放進去 stack 的數字，如果都是正、負數的話，就可以直接加總，麻煩的是遇到乘、除要怎麼處理？

因為我們需要知道乘、除後面的數字，才可以處理，但是如果是一直接連的乘、除就沒有關係，因為接連的乘、除都是符合四則運算的。

所以每當我們處理完一個數字的時候，我們要注意這個數字前面是加減號，還是乘除號？`sign` 就是幫助我們紀錄當下處理完的這個數字，他前面的四則運算符號是什麼，一開始預設是正號就好。

所謂的「處理完」數字還有兩種情況

1. 遇到了下一個四則運算符號
2. 走到最後一位數字

所以當處理完當下的數字後，這個數字前面的四則運算符號如果是遇上加減，直接放入到 stack 就好，遇上減號記得取負。

當處理完當下的數字之後，如果前面的數字是乘、除號，我們就要再把再前面的一個數字取出來計算完畢後，重新放回 Stack 中。

最後的答案就是加總。

```python
class Solution:
    def calculate(self, s: str) -> int:
        num, stack, sign = 0, [], "+"
        for i in range(len(s)):
            if s[i].isdigit():
                num = num * 10 + int(s[i])
            if s[i] in "+-*/" or i == len(s) - 1:
                if sign == "+":
                    stack.append(num)
                elif sign == "-":
                    stack.append(-num)
                elif sign == "*":
                    stack.append(stack.pop()*num)
                else:
                    stack.append(int(stack.pop()/num))
                num = 0
                sign = s[i]
        return sum(stack)
```
