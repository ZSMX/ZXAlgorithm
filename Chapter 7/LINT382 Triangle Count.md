# 382. Triangle Count

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.lintcode.com/problem/triangle-count/description

> 内容描述 Description

```
Given an array of integers, how many three numbers can be found in the array, so that we can build an triangle whose three edges length is the three numbers that we find?
Example 1:

Input: [3, 4, 6, 7]
Output: 3
Explanation:
They are (3, 4, 6), 
         (3, 6, 7),
         (4, 6, 7)
Example 2:

Input: [4, 4, 4, 4]
Output: 4
Explanation:
Any three numbers can form a triangle. 
So the answer is C(3, 4) = 4
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solutions/triangle-count/#tag-highlight-lang-python

```
class Solution:
    """
    @param S: A list of integers
    @return: An integer
    """
    def triangleCount(self, S):
        # write your code here
        if not S or len(S) < 3:
            return 0
        count = 0
        S.sort()
        for i in range(2, len(S)):
            left, right = 0, i - 1
            while left < right:
                value = S[left] + S[right]
                if value > S[i]:
                    count += right - left
                    right -= 1
                else:
                    left += 1
        return count
            
```