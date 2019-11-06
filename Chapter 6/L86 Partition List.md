###86. Partition List

题目： 
<https://leetcode.com/problems/partition-list/>


难度 : Medium

### Python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""
class Solution:
    """
    @param head: The first node of linked list.
    @param x: an integer
    @return: a ListNode 
    """
    def partition(self, head, x):
        # write your code here
        if head is None:
            return head
        aHead, bHead = ListNode(0), ListNode(0)
        aTail, bTail = aHead, bHead
        while head is not None:
            if head.val < x:
                aTail.next = head
                aTail = aTail.next
            else:
                bTail.next = head
                bTail = bTail.next
            head = head.next
        bTail.next = None
        aTail.next = bHead.next
        return aHead.next
```

### Java

思路一：


最简单的思路就是两个dummy head，然后一个指向 小于的node，一个指向大于的node


思路二：

不走寻常路了，使用两个指针，一个指向小于的尾巴，一个一直往后走，指向大于，然后交换node

完成比完美更重要啊，其实可以先试试用简单方法，因为我用我的不走寻常路画了比较久的图，写起来也稍显没那么美观，还在交换node的部分卡了一会



```
class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        dummy.next = head

        p1 = p2 = dummy

        while p1.next and p1.next.val < x:
            p1 = p1.next

        p2 = p1.next

        while p2:
            while p2.next and p2.next.val >= x:
                p2 = p2.next

            if p2.next == None:
                break
            node = p2.next
            p2.next = node.next
            node.next = p1.next
            p1.next = node
            p1 = p1.next

        return dummy.next
```