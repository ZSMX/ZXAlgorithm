###143. Reorder List

题目:

<https://leetcode.com/problems/reorder-list/>


难度:

Medium

### Python

https://leetcode.com/problems/reorder-list/discuss/44988/A-python-solution-O(n)-time-O(1)-space

```
# Splits in place a list in two halves, the first half is >= in size than the second.
# @return A tuple containing the heads of the two halves
def _splitList(head):
    fast = head
    slow = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next
        fast = fast.next

    middle = slow.next
    slow.next = None

    return head, middle

# Reverses in place a list.
# @return Returns the head of the new reversed list
def _reverseList(head):

  last = None
  currentNode = head

  while currentNode:
    nextNode = currentNode.next
    currentNode.next = last
    last = currentNode
    currentNode = nextNode

  return last

# Merges in place two lists
# @return The newly merged list.
def _mergeLists(a, b):

    tail = a
    head = a

    a = a.next
    while b:
        tail.next = b
        tail = tail.next
        b = b.next
        if a:
            a, b = b, a
            
    return head


class Solution:

    # @param head, a ListNode
    # @return nothing
    def reorderList(self, head):

        if not head or not head.next:
            return

        a, b = _splitList(head)
        b = _reverseList(b)
        head = _mergeLists(a, b)
```

```
# Concise version
def reorderList(self, head):
    if not head:
        return
        
    # find the mid point
    slow = fast = head 
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    # reverse the second half in-place
    pre, node = None, slow
    while node:
        pre, node.next, node = node, pre, node.next
    
    # Merge in-place; Note : the last node of "first" and "second" are the same
    first, second = head, pre
    while second.next:
        first.next, first = second, first.next
        second.next, second = first, second.next
    return 
```




取巧的办法是：

找到中间节点，断开，把后半截linked list reverse，然后合并 √

看了AC指南

```
class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        if head == None or head.next == None or head.next.next == None:
            return
        
        slow = head
        fast = head
        prev = None
        
        while fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next
            
        prev.next = None


        slow = self.reverseList(slow)
        
        cur = head
        while cur.next:
            tmp = cur.next
            cur.next = slow
            slow = slow.next
            cur.next.next = tmp
            cur = tmp
        cur.next = slow
            
        
    
    def reverseList(self,head):
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

