### 278. First Bad Version

<https://leetcode.com/problems/first-bad-version/>



难度 : Easy

Python

思路1：





思路2：

根据 search for a range 改的



```python
class Solution(object):
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        l, r = 0, n - 1
        while l <= r:
            mid = l + ((r - l) >> 2)
            if not isBadVersion(mid):
                l = mid + 1
            else:
                r = mid - 1
        return l
```





