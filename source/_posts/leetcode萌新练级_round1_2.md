---
title: LeetCode萌新练级_round1_2 两数相加 medium
date: 2018-10-11 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**两数相加**

> 给定两个非空链表来表示两个非负整数。位数按照逆序方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。
你可以假设除了数字 0 之外，这两个数字都不会以零开头。
示例：
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

**Add Two Numbers**

> You are given two **non-empty** linked lists representing two **non-negative** integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Example:
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

### 解题

这一题个人感觉主要考察的是对**链表**的理解

链表平时用不到，学了也忘了，偷瞄了一下答案怎么用，然后写出了代码
自己编写的代码
```Python3
class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        new_li = ListNode(0)

        alg_li, divisor = new_li, 0
        while l1 or l2:
            alg_val = divisor
            if l1:
                alg_val += l1.val
                l1 = l1.next
            if l2:
                alg_val += l2.val
                l2 = l2.next
            remainder = alg_val % 10 # 余数 1-9
            divisor = int(alg_val / 10) # 除数 0-1
            alg_li.next = ListNode(remainder)
            alg_li = alg_li.next
        if divisor == 1:
            alg_li.next = ListNode(1)
        return new_li.next
```
通过了所有测试用例

执行用时: **180 ms**, 在Add Two Numbers的Python3提交中击败了**38.16%** 的用户

时间复杂度：$O(max(m,n))$ m,n是l1,l2的长度

空间复杂度：$O(max(m,n))$

几次提交错误的原因，包括了没有考虑俩列长度不等，将表头也带入了。
这个代码时间复杂度和空间复杂度没什么大的差别，主要是初等数学的掌握

用了[网友的代码](https://github.com/kamyu104/LeetCode/tree/master/Python)，主要区别是他使用了divmod函数
```Python3
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        dummy = ListNode(0)
        current, carry = dummy, 0

        while l1 or l2:
            val = carry
            if l1:
                val += l1.val
                l1 = l1.next
            if l2:
                val += l2.val
                l2 = l2.next
            carry, val = divmod(val, 10)
            current.next = ListNode(val)
            current = current.next

        if carry == 1:
            current.next = ListNode(1)

        return dummy.next
```
时间复杂度：$O(max(m,n))$

空间复杂度：$O(max(m,n))$

执行用时: **156 ms**, 在Add Two Numbers的Python3提交中击败了**79.84%** 的用户
