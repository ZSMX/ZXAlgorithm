### 26. Remove Duplicates from Sorted Array



题目:
<https://leetcode.com/problems/remove-duplicates-from-sorted-array/>


难度:
Easy

思路：

### Python

区分Sorted和Unsorted，如果是sorted用一个pointer标识当前位置，如果是unsorted，还需要一个set来判断是否有重复的

> 思路1

https://leetcode.com/problems/remove-duplicates-from-sorted-array/discuss/11751/Simple-Python-solution-O(n)

```
class Solution:
    # @param a list of integers
    # @return an integer
    def removeDuplicates(self, A):
        if not A:
            return 0

        newTail = 0

        for i in range(1, len(A)):
            if A[i] != A[newTail]:
                newTail += 1
                A[newTail] = A[i]

        return newTail + 1
```

> 思路2

https://www.jiuzhang.com/solution/remove-duplicate-numbers-in-array/#tag-highlight-lang-python

```
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        
        new_tail = 0
        d = set()
       
        for i in range(0, len(nums)):
            if nums[i] not in d:
                d.add(nums[i])
                nums[new_tail] = nums[i]
                new_tail += 1
                
        return new_tail 
```







因为题目说了是```sorted array```，所以只需要不停判断当前位置值和下一位置是否相等，若相等则```pop掉当前值```，否则```move```到下一位置做重复判断


```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i = 0
        while i < (len(nums) - 1):
            if nums[i] == nums[i+1]:
                nums.remove(nums[i])
            else:
                i += 1
        return len(nums)
```


这里代码用```while loop```而不用```for loop```是因为```pop```操作之后```nums```的长度会变化

如：```for i in range(len(nums)-1)```实际上固定了```range```里面的值了，不会二次判断

```
n = 10
for i in range(n):
    n = n - 1  # 尽管n在变化
    print(i)

上面这段代码的输出结果为：

0
1
2
3
4
5
6
7
8
9
```


















