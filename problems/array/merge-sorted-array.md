# 88. Merge Sorted Array

[88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

### 從起始端到末端

{% tabs %}
{% tab title="Python" %}
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums1Copy = nums1[:m]

        i = 0
        j = 0
        k = 0

        while i < m and j < n:
            if nums1Copy[i] < nums2[j]:
                nums1[k] = nums1Copy[i]
                i += 1
            else:
                nums1[k] = nums2[j]
                j += 1
            k += 1

        if i == m:
            nums1[k:] = nums2[j:]
        if j == n:
            nums1[k:] = nums1Copy[i:]
```
{% endtab %}

{% tab title="Java" %}
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {

        int[] nums1Copy = new int[m];
        for (int i = 0; i < m; i++) {
            nums1Copy[i] = nums1[i];
        }

        int p1 = 0;
        int p2 = 0;

        for (int p = 0; p < m + n; p++) {
            if (p2 >= n || (p1 < m && nums1Copy[p1] < nums2[p2])) {
                nums1[p] = nums1Copy[p1++];
            } else {
                nums1[p] = nums2[p2++];
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

### 從末端到起始端

{% tabs %}
{% tab title="Python" %}
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        p1 = m - 1
        p2 = n - 1
        
        for p in reversed(range(m + n)):
            if p2 < 0:
                break
            if p1 >= 0 and nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
```
{% endtab %}

{% tab title="Java" %}
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1 = m - 1;
        int p2 = n - 1;
        
        for(int p = m + n - 1; p >= 0; p--) {
            if (p2 < 0) {
                break;
            }
            if (p1 >= 0 && nums1[p1] > nums2[p2]) {
                nums1[p] = nums1[p1--];
            } else {
                nums1[p] = nums2[p2--];
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

