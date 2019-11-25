# 604.Window Sum

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* http://www.lintcode.com/problem/window-sum/

> 内容描述 Description

```
Given an array of n integers, and a moving window(size k), move the window at each iteration from the start of the array, find the sum of the element inside the window at each moving.
Example 1

Input：array = [1,2,7,8,5], k = 3
Output：[10,17,20]
Explanation：
1 + 2 + 7 = 10
2 + 7 + 8 = 17
7 + 8 + 5 = 20
```
## 解题方案 Solutions
### Python

[https://www.jiuzhang.com/solutions/?search=window%20sum](https://www.jiuzhang.com/solutions/?search=window sum)

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    # @param nums {int[]} a list of integers
    # @param k {int} size of window
    # @return {int[]} the sum of element inside the window at each moving
    def winSum(self, nums, k):
        # Write your code here
        n = len(nums)
        if n < k or k <= 0:
            return []
        sums = [0] * (n - k + 1)
        for i in range(k):
            sums[0] += nums[i];

        for i in range(1, n - k + 1):
            sums[i] = sums[i - 1] - nums[i - 1] + nums[i + k - 1]

        return sums

```

