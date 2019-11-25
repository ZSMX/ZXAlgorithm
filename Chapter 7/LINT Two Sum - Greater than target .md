# Two Sum - Greater than target

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.jiuzhang.com/solutions/two-sum-greater-than-target/#tag-highlight-lang-python

> 内容描述 Description

```
Given an array of integers, find how many pairs in the array such that their sum is bigger than a specific target number. Please return the number of pairs.

在线评测地址: http://www.lintcode.com/problem/two-sum-greater-than-target/
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solutions/two-sum-greater-than-target/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    """
    @param nums: an array of integer
    @param target: An integer
    @return: an integer
    """
    def twoSum2(self, nums, target):
        n = len(nums)
        if n < 2:
            return 0
        
        nums.sort()
        
        res = 0
        l, r = 0, n - 1
        while l < r:
            if nums[l] + nums[r] <= target:
                l += 1
            else:
                res += r - l
                r -= 1
                
        return res
```

