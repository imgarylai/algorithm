# 989. Add to Array-Form of Integer

[989. Add to Array-Form of Integer](https://leetcode.com/problems/add-to-array-form-of-integer/)

```python
class Solution:
    def addToArrayForm(self, num: List[int], k: int) -> List[int]:
        num[-1] += k
        for i in reversed(range(len(num))):
            carry = num[i] // 10
            num[i] = num[i] % 10
            if i: 
                num[i-1] += carry
        while carry:
            num = [carry%10] + num
            carry = carry // 10
        return num
```
