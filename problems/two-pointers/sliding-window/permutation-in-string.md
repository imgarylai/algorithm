# 567. Permutation in String

[567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)

1. 我們需要想的是窗口增大的時候，需要更新哪些資訊？
   1. 如果 char 在目標內，增加計數
   2. 如果 char 的計數已經達到目標的計數，**valid 加一**
2. 何時要收縮窗口？
   1. 如果窗口的字串的長度已經大於目標的字串（因為我們要找的是 permutation\)
3. 收縮窗口時，需要更新哪些資訊？
   1. 檢查左邊的指針的字元在目標內
      1. 如果 char 的計數已經達到目標的計數，**valid 減一**
      2. 如果 char 在目標內，減少
4. 最終結果要在「擴大窗口」時更新還是「收縮窗口」時更新？
   1. 如果 valid 剛好和 target 的長度一樣的時候，代表找到 permutation 了，回傳 True 

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        target = Counter(list(s1))
        visited = defaultdict(int)
        left = 0
        right = 0
        valid = 0
        while right < len(s2):
            char = s2[right]
            right += 1
            if char in target:
                visited[char] += 1
                if visited[char] == target[char]:
                    valid += 1
            while right - left >= len(s1):
                if valid == len(target):
                    return True
                char = s2[left]
                left += 1
                if char in target:
                    if visited[char] == target[char]:
                        valid -= 1
                    visited[char] -= 1
        return False
```

