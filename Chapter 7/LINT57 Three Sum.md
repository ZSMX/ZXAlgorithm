# 57. Three Sum

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.lintcode.com/problem/3sum/description

> 内容描述 Description

```
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
Example 1:

Input:[2,7,11,15]
Output:[]
Example 2:

Input:[-1,0,1,2,-1,-4]
Output:	[[-1, 0, 1],[-1, -1, 2]]
```
## 解题方案 Solutions
### Python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    """
    @param numbers: Give an array numbers of n integer
    @return: Find all unique triplets in the array which gives the sum of zero.
    """
    def threeSum(self, nums):
        nums.sort()
        results = []
        length = len(nums)
        for i in range(0, length - 2):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            self.find_two_sum(nums, i + 1, length - 1, -nums[i], results)
        return results

    def find_two_sum(self, nums, left, right, target, results):
        while left < right:
            if nums[left] + nums[right] == target:
                results.append([-target, nums[left], nums[right]])
                right -= 1
                left += 1
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1
            elif nums[left] + nums[right] > target:
                right -= 1
            else:
                left += 1
```

