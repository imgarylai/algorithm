# 9. Palindrome Number

[9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

此題最簡單的解法會是把數字直接轉成字串，再透過字串處理，要注意的是如果是負數，直接不可能是回文，因為負號會直接影響回文的條件，一開始就可以剔除。

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0:
            return False
        s = str(x)
        left = 0
        right = len(s) - 1
        while left < right:
            if s[left] != s[right]:
                return False
            left += 1
            right -= 1
        return True
```

不過這個題目的精華並不是透過轉乘字串，而是要我們不能將題目給的整數轉換成字串。

直接用數字來思考，我如果有一個數字是 `32123` 我們可以怎麼處理？如下方的數字表示：

```text
32123 -> 3212, 3 -> 321, 32 -> 32, 321 -> ?
```

這就是題目要注意的地方，回文的題目在前言有提到過，回文的處理要很注意兩邊指針跨過邊界的情況，我們可以很明確地從上方的推論看到，當我們走到 `32, 123` 的時候，繼續往下走是沒有意義的，因為再走下去只會走回原路，如果是回文的話。所以這邊的終止條件應該是什麼呢？

先想想看雙指針，在雙指針的情況下，左邊的指針通常是比較小的指針，往大的方向走，右指針是比較大的指針，往小的方向走，一直到「跨越中線」。

在這個題目，其實可以重新這樣看：

```text
32123, 0 -> 3212, 3 -> 321, 32 -> 32, 321 -> 3, 3212 -> 0, 32123
```

用雙指針的概念來譬喻，就是左邊的指針比較大，往小的方向走，右邊的指針比較小，往大的方想走，終止條件是兩邊指針跨越邊界的同時，也就是**左邊的數小於或等於右邊的數**的時候，結束指針的移動。不過在這個題目裡面，我們並不會在指針移動的時候檢查，而是在指針移動結束後再檢查是不是回文。

根據上面的描述，這個題目就是屬於前面回文有提到的，需要考慮字串是**奇數或是偶數**個的題目，上面例子，跨越中線之後兩個數字並不是一樣的，但是好在我們知道一件事情，那就是跨越中線時，如果是奇數，中間的數字是完全不用考慮的，因為一個數字一定會滿足回文的條件。

在這裡的操作是，因為檢查回文一定要檢查到剛好跨越中線為止，所以我們就檢查到跨越中線，上面的例子就是`32, 321` ，那我們就把中間的數字剔除掉，把右邊的數字直接除以十就好。

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0 or (x % 10 == 0 and x != 0):
            return False
        left = x
        right = 0
        while left > right:
            right = right * 10 + left % 10
            left //= 10
        return left == right or left == right //10
```

寫到這裡，大致上了邏輯已經完成了，和字串相比，我們還少了最後的一個情況要考量，那就是如果有數字的結尾是 `0` ，也就是十的倍數，那也可以確定無法形成回文， 因為數字沒辦法以 `0` 做為開頭，但是如果是只有一個數字，那就是 `0` 本身，他也是十的倍數，那這個數字一定也是一個回文，所以 `0` 也是正確的回文，記得要剔除。
