# 1. Two Sum 两数之和

**<font color=red>难度: Easy</font>**

## 刷题内容

> 原题连接

* https://leetcode.com/problems/two-sum
* https://leetcode-cn.com/problems/two-sum/description

> 内容描述

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 解题方案

### Python

https://www.jiuzhang.com/solutions/two-sum/

> dict

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution(object):
    def twoSum(self, nums, target):
        #hash用于建立数值到下标的映射
        hash = {}
        #循环nums数值，并添加映射
        for i in range(len(nums)):
            if target - nums[i] in hash:
                return [hash[target - nums[i]], i]
            hash[nums[i]] = i
        #无解的情况
        return [-1, -1]
```

> two pointer

```
# 本参考程序来自九章算法，由 @布偶什么的就是布偶 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    """
    @param numbers: An array of Integer
    @param target: target = numbers[index1] + numbers[index2]
    @return: [index1 + 1, index2 + 1] (index1 < index2)
    """
    def twoSum(self, numbers, target):
        for i, a in enumerate(numbers):
            for j, b in enumerate(numbers[i + 1 - len(numbers):]):
                if a + b == target:
                    return [i, j + i + 1]
        return [-1, -1]
```





> 思路 1

可以用O(n^2) loop

但是也可以牺牲空间换取时间，异常聪明的AC解法

```
          2        7        11    15
         不存在   存在之中
lookup   {2:0}    [0，1]
```

* 建立字典 lookup 存放第一个数字，并存放该数字的 index
* 判断 lookup 种是否存在： `target - 当前数字`， 则表面 当前值和 lookup中的值加和为 target.
* 如果存在，则返回：  `target - 当前数字` 的 index 和 当前值的 index

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        lookup = {}
        for i, num in enumerate(nums):
            if target - num in lookup:
                return [lookup[target - num],i]
            lookup[num] = i
        return []
```
