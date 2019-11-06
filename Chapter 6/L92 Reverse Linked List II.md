###92. Reverse Linked List II 

题目:
<https://leetcode.com/problems/reverse-linked-list-ii/>

难度:
Medium

### Python

https://www.jiuzhang.com/solution/reverse-linked-list-ii/#tag-highlight-lang-python

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(1)
        dummy.next = head
        mth_prev = self.findkth(dummy, m - 1)
        mth = mth_prev.next
        nth = self.findkth(dummy, n)
        nth_next = nth.next
        nth.next = None
        self.reverse(mth)
        mth_prev.next = nth
        mth.next = nth_next
        return dummy.next
        
    def findkth(self, head, k):
        for i in range(k):
            if not head:
                return None
            head = head.next
        return head
    
    def reverse(self, head):
        cur = None
        while head:
            tmp = head.next
            head.next = cur
            cur = head
            head = tmp
        return head
```




跟 reverse linked list一样

思路： 找到 第 m 个node，然后开始reverse到第n个node，然后再把它们和原本的list连接起来

AC 代码

```
class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        # m == n, not reverse
        if m == n : return head

        dummy = ListNode(-1)
        dummy.next = head

        mbefore = dummy
        cnt = 1
        
        while mbefore and cnt < m:
            mbefore = mbefore.next
            cnt += 1

        prev = None
        cur = mbefore.next
        tail1 = mbefore.next
        

        while cnt <= n :
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
            cnt += 1



        mbefore.next = prev
        tail1.next = cur

        return dummy.next 
```

看了一下别人的代码，又比我写的好嘛，因为是保证m和n有效，用的是for循环先找到 m node:


	for _ in range(m-1):
		....
		
	for _ in range(n-m):
		reverse 操作