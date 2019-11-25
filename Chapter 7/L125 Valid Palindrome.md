### 125. Valid Palindrome

题目:
<https://leetcode.com/problems/valid-palindrome/>


难度:

Easy

### Python

https://www.jiuzhang.com/solution/valid-palindrome/#tag-highlight-lang-python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    # @param {string} s A string
    # @return {boolean} Whether the string is a valid palindrome
    def isPalindrome(self, s):
        start, end = 0, len(s) - 1
        while start < end:
            while start < end and not s[start].isalpha() and not s[start].isdigit():
                start += 1
            while start < end and not s[end].isalpha() and not s[end].isdigit():
                end -= 1
            if start < end and s[start].lower() != s[end].lower():
                return False
            start += 1
            end -= 1
        return True
```



就是比较reversed string 和原本的是否相等.


```python
class Solution(object):
    def isPalindrome(self,s):
        """
        :type s: str
        :rtype: bool
        """
          
        new=[]  
        s = s.lower()  
  
        for i in s:  
            if '0'<=i<='9' or 'a'<=i<='z':  
                new.append(i)  
  
        return new == new[::-1]  
```

或者用正则,详见[re.sub()用法](http://blog.csdn.net/geekleee/article/details/75309433)
瞬间```beats 97.71%```
```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        newString = re.sub("[^0-9a-zA-Z]+", "", s)
        return newString.lower() == newString.lower()[::-1]
```

