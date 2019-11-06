# Search in a Big Sorted Array

**<font color=red>难度: Medium</font>**

## 刷题内容

> 原题连接

* https://www.jiuzhang.com/solutions/search-in-a-big-sorted-array/

> 内容描述

```

Given a big sorted array with non-negative integers sorted by non-decreasing order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by ArrayReader.get(k) (or ArrayReader->get(k) for C++).

Find the first index of a target number. Your algorithm should be in O(log k), where k is the first index of the target number.

Return -1, if the number doesn't exist in the array.

在线评测地址: http://www.lintcode.com/problem/search-in-a-big-sorted-array/
```
## 解题方案
### Python

> 思路 1

**方法1 倍增:**

首先特判一下首个元素. 然后设定 `idx = 0` 为查找的下标, `jump = 1` 为向后跳跃的长度.

每次循环将 `idx` 向后移动 `jump` 个元素, 并将 `jump` 翻倍. 而如果移动后的位置不小于 `target`, 则 `jump` 缩小至一半.

即我们在保证每次跳跃后的 `idx` 的位置都小于`target`的前提下, 倍增式地跳跃, 以此保证 O(logn) 的时间复杂度.

循环终止的条件就是 `jump == 0`, 就是说, 这时 `idx + 1` 的位置以及不小于 `target` 了 (此时idx位置的仍然是小于target)

也就是说, 到最后`idx`指向的元素是: 最大的小于`target`的元素. 返回答案前判断一下 `idx + 1` 是否 `target` 即可.

> 思路 2

**方法2 二分:**

二分查找第一个不小于`target`的元素很简单. 但是需要确定二分区间的范围. 此时还是需要倍增地找到右边界.

初始右边界为1, 如果右边界的数小于 `target`, 就将其倍增, 直到右边界不小于`target`.

这时就可以二分查找了.

注意: 越界访问是没有关系的, 因为这个`ArrayReader`在越界访问时, 返回 INT_MAX, 一定不小于 `target`. 而即使是返回 -1 之类的数值, 我们也可以加一个判断搞定.


```python
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


############# 方法1 倍增

"""
Definition of ArrayReader
class ArrayReader(object):
    def get(self, index):
        # return the number on given index, 
        # return 2147483647 if the index is invalid.
"""
class Solution:
    """
    @param: reader: An instance of ArrayReader.
    @param: target: An integer
    @return: An integer which is the first index of target.
    """
    def searchBigSortedArray(self, reader, target):
        firstElement = reader.get(0)
        if firstElement == target:
            return 0
        elif firstElement > target:
            return -1
        
        idx, jump = 0, 1
        while jump:
            while jump and reader.get(idx + jump) >= target:    # 越界时返回INT_MAX, 必然不小于target
                jump >>= 1
            idx += jump
            jump <<= 1      # 当jump为0时, 左移一位不影响它的值, 不影响循环结束
        
        if reader.get(idx + 1) == target:
            return idx + 1
        else:
            return -1
        
########## 方法2 二分

"""
Definition of ArrayReader
class ArrayReader(object):
    def get(self, index):
    	# return the number on given index, 
        # return 2147483647 if the index is invalid.
"""
class Solution:
    """
    @param: reader: An instance of ArrayReader.
    @param: target: An integer
    @return: An integer which is the first index of target.
    """
    def searchBigSortedArray(self, reader, target):
        l, r = 0, 1
        while reader.get(r) < target:
            r <<= 1
        
        while (l < r):
            mid = (l + r) >> 1
            if reader.get(mid) >= target:
                r = mid
            else:
                l = mid + 1
        
        if reader.get(l) == target:
            return l
        else:
            return -1
```

​    


