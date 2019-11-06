### 206. Reverse Linked List

题目:
<https://leetcode.com/problems/reverse-linked-list/>

难度:
Easy

### Python

2(cur)->1
3(head)->4(head.next)->5

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:

    def reverse(self, head):
        #curt表示前继节点
        curt = None
        while head != None:
            #temp记录下一个节点，head是当前节点
            temp = head.next
            head.next = curt
            curt = head
            head = temp
        return curt
```



用三个指针，分别指向prev，cur 和 nxt，然后loop一圈还算比较简单.




```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None 
        cur = head
        while(cur):
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        return prev
```
其实一个指针就够了
```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        prev = None
        while head.next:
            tmp = head.next
            head.next = prev
            prev = head
            head = tmp
        head.next = prev  
        return head
```

递归版本，可以再消化一下.


```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        return self.reverseHelper(head, None)
    
    def reverseHelper(self, head, new_head):
        if not head:
            return new_head
        nxt = head.next
        head.next = new_head
        return self.reverseHelper(nxt, head)
```
