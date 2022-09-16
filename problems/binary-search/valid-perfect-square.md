# 367. Valid Perfect Square

[367. Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

{% tabs %}
{% tab title="Python" %}
```python
class Solution:
    def isPerfectSquare(self, num: int) -> bool:  
        if num == 1:
            return True
        left = 1
        right = num // 2

        while left <= right:
            mid = left + (right - left) // 2
            square = mid * mid
            if square == num:
                return True
            elif square > num:
                right = mid - 1
            elif square < num:
                left = mid + 1

        return False
```
{% endtab %}

{% tab title="Java" %}
{% code lineNumbers="true" %}
```java
class Solution {
    public boolean isPerfectSquare(int num) {
        if (num == 1) {
            return true;
        }
        long left = 1;
        long right = num / 2;
        long mid, square;
        while(left <= right) {
            mid = left + (right - left) / 2;
            square = mid * mid;
            if (square == num) {
                return true;
            } else if (square > num) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return false;
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
