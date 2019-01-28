---
title: LeetCode萌新练级_round1_19 删除链表的倒数第N个节点 medium
date: 2018-11-12 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**删除链表的倒数第N个节点**

> 给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
```
示例：
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：
给定的 n 保证是有效的。
进阶：
你能尝试使用一趟扫描实现吗？
```

**Romove Nth Node From End of List**

> Given a linked list, remove the n-th node from the end of list and return its head.
```
Example:
Given linked list: 1->2->3->4->5, and n = 2.
After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:
Given n will always be valid.
Follow up:
Could you do this in one pass?
```

### 解题

这一题题目有提到，能不能只扫描一遍就实现，这个题其实一开始就是有思路的，就是扫描的时候，从最开始就让游标定在当前链的前n个数，当遇到结尾时，就将此时的游标节点跳过，只可惜不太会写链表，偷瞄了一下答案的写法，然后按照自己的思路，实现了。
```Python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        fast = slower = head
        for i in range(n):
            fast = fast.next
        while not fast:
            return head.next
        while fast.next:
            slower = slower.next
            fast = fast.next
        slower.next = slower.next.next
        return head
```
时间复杂度：$O(n)$
空间复杂度：$O(1)$

执行用时: **56 ms**, 在Remove Nth Node From End of List的Python3提交中击败了**72.69%** 的用户


再看看答案中排名靠前的运行结果
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        if not head or n<1:
            return None
        fast=head
        slow=head
        for _ in range(n):
            if not fast:
                return None
            fast=fast.next
        if not fast:
            return head.next
        while fast.next:
            fast=fast.next
            slow=slow.next
        slow.next=slow.next.next
        return head
```

执行用时: **48 ms**, 在Remove Nth Node From End of List的Python3提交中击败了**99.57%** 的用户

将特殊情况放在最前面判断，一点点的细节，都会提高执行速度_(:зゝ∠)_
