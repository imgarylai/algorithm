# 866. Prime Palindrome

[866. Prime Palindrome](https://leetcode.com/problems/prime-palindrome/)

[9. Palindrome Number](palindrome-number.md) 和 [204. Count Primes](../../problems/math/count-primes.md) 的結合。

```python
class Solution:

    def isPalindrome(self, n):
        if n < 0 or (n % 10 == 0 and n != 0):
            return False
        left = n
        right = 0
        while left > right:
            right = right * 10 + left % 10
            left //= 10
        return left == right or left == right //10

    def isPrimeNumber(self, n):
        return n > 1 and all(n % d for d in range(2, int(n**.5) + 1))

    def primePalindrome(self, n: int) -> int:
        while True:
            if self.isPalindrome(n) and self.isPrimeNumber(n):
                return n
            n += 1
            if 10**7 < n < 10**8:
                n = 10**8
```

