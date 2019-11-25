# 39.Recover rotated sorted array

**<font color=red>难度: Easy</font>**

## 刷题内容 Question

> 原题连接 Link

* https://www.lintcode.com/problem/recover-rotated-sorted-array/description

> 内容描述 Description

```
Given a rotated sorted array, recover it to sorted array in-place.（Ascending）
Example1:
[4, 5, 1, 2, 3] -> [1, 2, 3, 4, 5]
Example2:
[6,8,9,1,2] -> [1,2,6,8,9]

Challenge
In-place, O(1) extra space and O(n) time.
```
## 解题方案 Solutions
### Python

https://www.jiuzhang.com/solution/recover-rotated-sorted-array/#tag-highlight-lang-java

```
class Solution:
    """
    @param nums: An integer array
    @return: nothing
    """
    def recoverRotatedSortedArray(self, nums):
        # write your code here
        if not nums:
            return nums
        
        for i in range(len(nums) - 1):
            if nums[i] > nums[i + 1]:
                self.reverse(nums, 0, i)
                self.reverse(nums, i + 1, len(nums) - 1)
                self.reverse(nums, 0, len(nums) - 1)
    
    def reverse(self, nums, left, right):
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
```

