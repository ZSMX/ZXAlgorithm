# 8.Rotate String

**<font color=red>难度: Easy</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.lintcode.com/problem/rotate-string/description

> 内容描述 Description

```
Given a string(Given in the way of char array) and an offset, rotate the string by offset in place. (rotate from left to right).

Example 1:

Input: str="abcdefg", offset = 3
Output: str = "efgabcd"	
Explanation: Note that it is rotated in place, that is, after str is rotated, it becomes "efgabcd".
Example 2:

Input: str="abcdefg", offset = 0
Output: str = "abcdefg"	
Explanation: Note that it is rotated in place, that is, after str is rotated, it becomes "abcdefg".
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solution/rotate-string/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    # @param s: a list of char
    # @param offset: an integer 
    # @return: nothing
    def rotateString(self, s, offset):
        # write you code here
        if len(s) > 0:
            offset = offset % len(s)
            
        temp = (s + s)[len(s) - offset : 2 * len(s) - offset]

        for i in xrange(len(temp)):
            s[i] = temp[i]

```

