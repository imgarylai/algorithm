# n Sum 問題

* 1. [2 Sum](https://leetcode.com/problems/two-sum/)
* [15. 3 Sum](3sum.md)
* [18. 4 Sum](4sum.md)
* [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
* [170. Two Sum III - Data structure design](https://leetcode.com/problems/two-sum-iii-data-structure-design/)
* [454. 4 Sum II](4-sum-ii.md)
* [653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)
* [1099. Two Sum Less Than K](https://leetcode.com/problems/two-sum-less-than-k/)
* [1679. Max Number of K-Sum Pairs](https://leetcode.com/problems/max-number-of-k-sum-pairs/)

Two sum 最簡單的就是用窮舉法把所有的組合都列出來，時間複雜度為 `O(n^2)`，而且一直到 n sum 都可以使用這樣的方式來做。當然就是時間複雜度太高了。

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return [-1, -1]
```

如果題目的陣列是有序排列的陣列，也可以使用雙指針來找到。這個方法很重要是因為在未來要拓展到 nSum 時，我們需要要知道這個解法，那當然如果是無序排列的陣列，也可以先排序，再開始透過雙指針的方式去找到所有的答案。

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        def helper(numbers: List[int], target: int):
            lo = 0
            hi = len(numbers) - 1
            while lo < hi:
                s = nums[lo] + nums[hi]
                if s < target:
                    lo += 1
                elif s > target:
                    hi -= 1
                else: # s == target
                    res.append([left, right])
            return res
        numbers.sort()
        return helper(numbers, target)
```

於是這樣就可以開始擴展當 `n > 2` 的時候， 該怎麼辦呢？

* 當 `n == 1` 的時候，沒有所謂的總和問題，所以答案為**空集合。**
* 當 `n == 2` 的時候，就是所謂的 **2 Sum** ，可以透過上方的方式找到
* 當 `n == 3` 的時候，是不是可以把設定的目標先剪去第一個陣列中的第 `i` 個數字，得到一個新目標，接著在剩下的兩個陣列中，用新的目標找 **2 Sum** 。
* ...
* 當 `n == k` 的時候，就可以推導出，先將目標減去第一個陣列中的第 `i` 個數字，得到一個新目標後，在接下來的 k - 1 個陣列中，找出 **k-1 Sum** 。

所以我們就找到了基本情況， `n == 1` 與 `n == 2`，並且可以透過遞迴的方式來找出 nSum 。

```python
class Solution:
    def twoSum(self, nums: List[int], start: int, target: int) -> List[List[int]]:
        lo = start
        hi = len(nums) - 1
        res = []
        while lo < hi:
            left = nums[lo]
            right = nums[hi]
            s = nums[lo] + nums[hi]
            if s < target:
                lo += 1
            elif s > target:
                hi -= 1
            else: # s == target
                res.append([left, right]) 
                while (lo < hi and left == nums[lo]):
                    lo += 1
                while (lo < hi and right == nums[hi]):
                    hi -= 1
        return res

    def kSum(self, k, nums, target, start):
        size = len(nums)
        res = []
        if n < 2 or size < k:
            return res
        if n == 2:
            return self.twoSum(nums, start, target)
        else:
            i = start
            while i < size:
                tuples = self.kSum(nums, k - 1, i + 1, target - nums[i])
                for tup in tuples:
                    tup.append(nums[i])
                    res.append(tup)
                while i < size - 1 and nums[i] == nums[i + 1]:
                    i += 1
                i += 1
        return res


    def nSum(self, nums: List[int], target: int, n: int) -> List[List[int]]:
        # 先一開始就將陣列排序
        nums.sort()
        return self.kSum(n, nums, target, 0)
```

而 nSum 其實還有另外一個觀念還沒有寫到，那就是利用 Hash Table ，讓我們重回到 2 Sum ，2 Sum 是 LeetCode 的天字第一號題目，又是一個超高頻的題目，我想幾乎每個人都會，雙指針的方式在原始的 2 Sum 題目裡面，其實不是最有效率的，另一個方法不會太難，儘管是簡單的題目，但我在第一次刷題的時候，記得想出這個方法的時候心裡還是有一種「哇！原來這就是刷題的感覺啊，所有的東西我都會，都很常用，但是第一次要把他們用在一起的時候，是沒辦法瞬間做到的」

使用 Hash Table 的原理很簡單，那就是我們在遍歷陣列中的每個元素的時候，將目標減去當下的值得到的餘值，**「回」**去 Hash Table 裡面找，看看這個餘值有沒有在裡面，如果有的話，代表在迭代到當下這個數字「之前」，有一個數字就是這個餘值，而這個餘值的座標就是我們要的第一個座標。為什麼會在之前呢？因為上面這個步驟，我們透過餘值在 Hash Table 找的時候，如果沒有餘值，我們就把當下的數字做為 key 放進去 Hash Table 裡面，並將其 value 設定為陣列的指標。

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        table = {}
        for i in range(len(nums)):
            num = nums[i]
            if target - num in table:
                return [table[target - num], i]
            else:
                table[num] = i
```

Hash Table 在 LeetCode 的很多題目裡面，扮演著很重要的角色，因為 Hash Table 可以很高效的讓我們儲存值，並記錄很多的資訊，而且可以快速的找到我們要的答案，這個方法好是好在我們不用重新排序陣列，又或是題目如果限制我們對陣列的排序的時候可以用。

而這個解法，我們就可以挑戰解 454. 4 Sum II 的概念，在這個題目裡面，題目給我們的是給定四個陣列，從四個陣列中各挑一個數字，其總和要等於給定的目標。

因為這個問題我們就不能對陣列做排序，所以就要嘗試的去想是不是能用 Hash Table 來解決問題，我一開始想到的是分治法來解決，但是想到的問題是，前兩個陣列任意各挑一個總和為零，後兩個陣列任意各挑一個數字總和為零，只是這個問題的答案的一部分集合，因為前兩個陣列任意各挑一個總和為二，後兩個陣列任意各挑一個數字總和為負二，答案也是零，這裡就是這個題目比較難的地方，也就是說。

```text
# 這是真正的目標
a + b == -(c+d)
# 這只是一小部分的答案
a + b == (c+d) == 0
```

那就是我們還是可以將四個陣列分成兩個兩個看，不過我們要用 Hash Table 要紀錄的是，前兩個陣列，任意兩數字總和的計數，那後面其實就很簡單了，接下來後面兩個陣列，各任意取一個數的總和取負，如果有在 Hash Table 中，就代表了前兩個陣列各任意取一個數的總和，與後兩個陣列各任意取一個數的總和，相等於目標，題目就可以這樣解：

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        table = {}
        ans = 0
        for num1 in nums1:
            for num2 in nums2:
                s = num1 + num2
                table[s] = table.get(s, 0) + 1

        for num3 in nums3:
            for num4 in nums4:
                s = num3 + num4
                if -s in table:
                    ans += table.get(-s, 0)

        return ans
```

可以稍微的整理一下，變成不一定要是只能是 0 任意目標，任意目標皆可

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        def helper(nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int], target: int):
            table = {}
            ans = 0
            for num1 in nums1:
                for num2 in nums2:
                    s = num1 + num2
                    table[s] = table.get(s, 0) + 1

            for num3 in nums3:
                for num4 in nums4:
                    s = num3 + num4
                    if target-s in table:
                        ans += table.get(target-s, 0)

            return ans
        return helper(nums1, nums2, nums3, nums4, 0)
```

## 總結

其實一道 nSum 題目就涵括了幾個概念

1. 如何透過雙指針來逼近我們需要的目標。
2. 雙指針在操作的時候要如何迴避掉不需要的值？在此範例我們要找出所有可以達成 nSum 的**「值」**，如果有重複出現的答案時，我們要跳過。（程式碼 L16-L19 的範圍）
3. 遞迴的觀念，在一般的題目裡面，通常基本情況是一個固定的值，但在這裡基本情況其實是要解一個 2 Sum 的，在有些 LeetCode 的困難的題目，有時候遞迴的基本情況是是要靠程式的運算出來的。
4. 除了雙指針與遞迴，我們也可以透過 Hash Table 來完成 2 Sum 的問題。

