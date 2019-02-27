---
title: LeetCode萌新练级_round1_9 回文数 easy
date: 2018-10-18 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**回文数**

> 判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
```
示例 1:
输入: 121
输出: true

示例 2:
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

示例 3:
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```
**进阶:
你能不将整数转为字符串来解决这个问题吗？**

**Palindrome Number**

> Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
```
Example 1:
Input: 121
Output: true

Example 2:
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

Example 3:
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

### 解题

一遍过，不过耗时还是有点多
```Python3
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if str(x) == str(x)[::-1]:
            return True
        else:
            return False
```

时间复杂度：$O(n)$
空间复杂度：$O(1)$

执行用时: **440 ms**, 在Palindrome Number的Python3提交中击败了**30.44%** 的用户

再考虑进阶要求，不使用字符串的方式解决
```
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        y = 0
        if x < 0 or (x % 10 == 0  and x != 0):
            return False
        while x > y:
            y = y * 10 + x % 10
            x = int(x / 10)
        return x == y or x == int(y / 10)
```
时间复杂度：$O(log_{10}(n))$(官方说这个时间复杂度是这样，但我觉得时间复杂度应该是$O(\frac{1}{2}log_{10}(n))$)
空间复杂度：$O(1)$

执行用时: **408 ms**, 在Palindrome Number的Python3提交中击败了**51.63%** 的用户
这里参考了官方的题解，反转其中一半的数字，通过求余和求除的方法，如果反转得到的数字与剩余的数字相等，就说明数字是回文数(奇数会考虑再除以10)，这样比反转整个数字时间要减少一半。

看[网友的代码](https://github.com/apachecn/awesome-algorithm/tree/master/docs/Leetcode_Solutions/Python)的时候发现，这道题以前是medium，现在难度已经变成easy了。
```Python3
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0 or (x != 0 and x % 10 == 0):
            return False
        rev, y = 0, x
        while x > 0:
            rev = rev * 10 + x % 10
            x = int(x / 10)
        return y == rev
```
时间复杂度：$O(log_{10}(n))$
空间复杂度：$O(1)$

执行用时: **328 ms**, 在Palindrome Number的Python3提交中击败了**83.72%** 的用户

感觉很奇怪反转整个数字执行用时比反转一半时间短。。。。不是很明白。
