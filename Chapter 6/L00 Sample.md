# 78. Subsets

**<font color=red>难度: Medium</font>**

## 刷题内容 Question

> 原题连接 Link

* https://leetcode.com/problems/subsets/description/

> 内容描述 Description

```

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
## 解题方案 Solutions
### Python

> 思路 1

每次拿一个，跟res里面的每一个已有列表取并集再次插入res中

```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = [[]]
        for num in nums:
            res.extend([tmp+[num] for tmp in res])
        return res     
```

> 思路 2

BackTrack 标准解法版

对每个元素，有两种可能，加入 cur_lst 和不加入 cur_lst，写起来思路还是很清爽的


```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        res = []
        
        def search(cur_lst, idx):
            if idx == len(nums):
                res.append(cur_lst)
                return
            search(cur_lst + [nums[idx]], idx + 1)
            search(cur_lst, idx + 1)
        
        search([], 0)
        return res
```


> 思路 3

DFS

```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        res = []
        def dfs(depth, start, lst):
            res.append(lst)
            if depth == len(nums):
                return
            for i in range(start, len(nums)):
                dfs(depth+1, i+1, lst+[nums[i]])
        dfs(0, 0, [])
        return res      
```


