# 680. Valid Palindrome II

**<font color=red>难度: Easy</font>**

## 刷题内容 Question

> 原题连接 Link

* https://leetcode.com/problems/valid-palindrome-ii/

> 内容描述 Description

```
Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.

Example 1:
Input: "aba"
Output: True
Example 2:
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
Note:
The string will only contain lowercase characters a-z. The maximum length of the string is 50000.
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solution/valid-palindrome-ii/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @令狐冲 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    """
    @param s: a string
    @return: nothing
    """
    def validPalindrome(self, s):
        left, right = self.twoPointer(s, 0, len(s) - 1)            
        if left >= right:
            return True
            
        return self.isPalindrome(s, left + 1, right) or self.isPalindrome(s, left, right - 1)

    def isPalindrome(self, s, left, right):
        left, right = self.twoPointer(s, left, right)
        return left >= right
        
    def twoPointer(self, s, left, right):
        while left < right:
            if s[left] != s[right]:
                return left, right
            left += 1
            right -= 1
        return left, right
```

