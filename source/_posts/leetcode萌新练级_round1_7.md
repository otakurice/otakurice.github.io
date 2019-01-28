---
title: LeetCode萌新练级_round1_7 反转整数 easy
date: 2018-10-16 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**反转整数**

> 给定一个 32 位有符号整数，将整数中的数字进行反转。
```
示例 1:
输入: 123
输出: 321

示例 2:
输入: -123
输出: -321

示例 3:
输入: 120
输出: 21
```
注意:
假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。根据这个假设，如果反转后的整数溢出，则返回 0。

**Longest Palindromic Substring**

> Given a 32-bit signed integer, reverse digits of an integer.
```
Example 1:
Input: 123
Output: 321

Example 2:
Input: -123
Output: -321

Example 3:
Input: 120
Output: 21
```
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

### 解题

这一题还是比较简单的，用了递归的方法，一开始没有设置溢出，设置溢出后，代码就通过了。
```Python3
class Solution:
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        i = 1
        if x < 0:
            return -self.reverse(-x)
        elif int(x / 10) == 0:
            return  x
        y = x % 10
        res = y * 10**(len(str(x)) -1) + self.reverse(int(x/10))
        return res if res < 0x7fffffff else 0
```

时间复杂度：$O(log(x))$

空间复杂度：$O(1)$

执行用时: **88 ms**, 在Reverse Integer的Python3提交中击败了**22.61%** 的用户

[网友的代码](https://github.com/apachecn/awesome-algorithm/tree/master/docs/Leetcode_Solutions/Python)(有一点小错误，我修改了一下)
```Python3
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x < 0:
            return -self.reverse(-x)
        res = 0
        while x:
            res = res * 10 + x % 10
            x = int(x / 10)
        return res if res <= 0x7fffffff else 0
```
时间复杂度：$O(log(x))$

空间复杂度：$O(1)$

这个代码总体和我写的差不多，只是直接使用while来解决了迭代问题

执行用时: **80 ms**, 在Reverse Integer的Python3提交中击败了**52.68%** 的用户

另一种方法，其实我也想到了，但我觉得不至于用这种方法
```
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """    
        x = -int(str(x)[::-1][:-1]) if x < 0 else int(str(x)[::-1])   # [:-1]相当于把负号去掉
        x = 0 if abs(x) > 0x7FFFFFFF else x
        return x
```

结果这种方法居然更快，这里是将数字转换成了字符串

执行用时: **72 ms**, 在Reverse Integer的Python3提交中击败了**81.16%** 的用户
