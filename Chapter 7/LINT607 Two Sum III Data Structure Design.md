# 607. Two sum data structure design

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.lintcode.com/problem/two-sum-iii-data-structure-design/description

> 内容描述 Description

```
Design and implement a TwoSum class. It should support the following operations: add and find.

add - Add the number to an internal data structure.
find - Find if there exists any pair of numbers which sum is equal to the value.
add(1); add(3); add(5);
find(4) // return true
find(7) // return false
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solution/two-sum-iii-data-structure-design/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class TwoSum(object):

    def __init__(self):
        # initialize your data structure here
        self.count = {}
        

    # Add the number to an internal data structure.
    # @param number {int}
    # @return nothing
    def add(self, number):
        # Write your code here
        if number in self.count:
            self.count[number] += 1
        else:
            self.count[number] = 1

        

    # Find if there exists any pair of numbers which sum is equal to the value.
    # @param value {int}
    # @return true if can be found or false
    def find(self, value):
        # Write your code here
        for num in self.count:
            if value - num in self.count and \
                (value - num != num or self.count[num] > 1):
                return True
        return False
        


# Your TwoSum object will be instantiated and called as such:
# twoSum = TwoSum()
# twoSum.add(number)
# twoSum.find(value)
```

