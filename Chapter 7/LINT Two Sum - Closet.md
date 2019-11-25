# Two Sum Closest

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.jiuzhang.com/solutions/two-sum-closest/#tag-highlight-lang-python

> 内容描述 Description

```
给定整数数组num，从中找到两个数字使得他们和最接近target，返回两数和与 target 的差的 绝对值。
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solutions/two-sum-closest/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    # @param {int[]} nums an integer array
    # @param {int} target an integer
    # @return {int} the difference between the sum and the target
    def twoSumClosest(self, nums, target):
        # Write your code here
        nums.sort()
        i, j = 0, len(nums)  - 1

        diff = 0x7fffffff
        while i < j:
            if nums[i] + nums[j] < target:
                diff = min(diff, target - nums[i] - nums[j])
                i += 1
            else:
                diff = min(diff, nums[i] + nums[j] - target)
                j -= 1

        return diff
```