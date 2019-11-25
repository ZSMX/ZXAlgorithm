# Three Sum Closest

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.jiuzhang.com/solutions/3sum-closest/#tag-highlight-lang-python

> 内容描述 Description

```
给一个包含 n 个整数的数组 S, 找到和与给定整数 target 最接近的三元组，返回这三个数的和。
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solutions/3sum-closest/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    """
    @param numbers: Give an array numbers of n integer
    @param target: An integer
    @return: return the sum of the three integers, the sum closest target.
    """
    def threeSumClosest(self, numbers, target):
        numbers.sort()
        ans = None
        for i in range(len(numbers)):
            left, right = i + 1, len(numbers) - 1
            while left < right:
                sum = numbers[left] + numbers[right] + numbers[i]
                if ans is None or abs(sum - target) < abs(ans - target):
                    ans = sum
                    
                if sum <= target:
                    left += 1
                else:
                    right -= 1
        return ans
```