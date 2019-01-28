---
title: LeetCode萌新练级_round1_21 合并两个有序链表 easy
date: 2018-11-20 11:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**合并两个有序链表**

> 将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。
```
示例：
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

**Merge Two Sorted Lists**

> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
```
Example:
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

### 解题

这一题还是挺简单的，就是始终记不住链表的使用//(ㄒoㄒ)//~~
```Python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        a = b = ListNode(0)
        while l1 and l2:
            if l1.val <= l2.val:
                b.next = l1
                l1 = l1.next
            else:
                b.next = l2
                l2 = l2.next
            b = b.next
        if l1 or l2:
            b.next = l1 or l2
        return a.next
```
时间复杂度：$O(len(l1+l2))$
空间复杂度：$O(1)$

执行用时: **56 ms**, 在Merge Two Sorted Lists的Python3提交中击败了**95.89%** 的用户

官方排行里的代码，运行了之后时间还不如我自己写的(摊手)
