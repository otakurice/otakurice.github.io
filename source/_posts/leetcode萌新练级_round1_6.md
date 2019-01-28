---
title: LeetCode萌新练级_round1_6 Z字形变换 medium
date: 2018-10-15 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**Z字形变换**

> 将字符串 "PAYPALISHIRING" 以Z字形排列成给定的行数：
P   A   H   N
A P L S I I G
Y   I   R
之后从左往右，逐行读取字符："PAHNAPLSIIGYIR"
实现一个将字符串进行指定行数变换的函数:
string convert(string s, int numRows);
```
示例 1:
输入: s = "PAYPALISHIRING", numRows = 3
输出: "PAHNAPLSIIGYIR"

示例 2:
输入: s = "PAYPALISHIRING", numRows = 4
输出: "PINALSIGYAHRPI"
解释:
P     I    N
A   L S  I G
Y A   H R
P     I
```

**Longest Palindromic Substring**

> The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:
string convert(string s, int numRows);
```
Example 1:
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"

Example 2:
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
```

### 解题

代码还是写出来了，但是执行时间不够满意。
```Python3
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        li = []
        if numRows == 1:
            return s
        for i in range(numRows):
            a = i
            while a < len(s):
                if i == 0 or i == numRows - 1:
                    li.append(s[a])
                else:
                    li.append(s[a])
                    if a + 2*numRows - 2 - 2*i < len(s):
                        li.append(s[a + 2*numRows - 2 - 2*i])
                a += 2 * numRows -2
        return ''.join(li)
```

时间复杂度：$O(n)$

空间复杂度：$O(n)$

执行用时: **176 ms**, 在ZigZag Conversion的Python3提交中击败了**26.93%** 的用户

[网友的代码](https://github.com/apachecn/awesome-algorithm/tree/master/docs/Leetcode_Solutions/Python)
```Python3
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1 or numRows >= len(s):
            return s
        res = [''] * numRows
        idx, step = 0, 1
        for x in s:
            res[idx] += x
            if idx == 0:  ## 第一行，一直向下走
                step = 1
            elif idx == numRows - 1: ## 最后一行了，向上走
                step = -1
            idx += step
        return ''.join(res)
```
时间复杂度：$O(n)$
空间复杂度：$O(n)$

这个代码总体和我写的差不多，只是直接使用while来解决了迭代问题

执行用时: **92 ms**, 在ZigZag Conversion的Python3提交中击败了**99.51%** 的用户

根据这个我又优化了自己的代码
```Python3
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        li = [''] * numRows
        if numRows == 1:
            return s
        for i in range(numRows):
            a = i
            while a < len(s):
                if i == 0 or i == numRows - 1:
                    li[i] += s[a]
                else:
                    li[i] += s[a]
                    if a + 2*numRows - 2 - 2*i < len(s):
                        li[i] += s[a + 2*numRows - 2 - 2*i]
                a += 2 * numRows -2
        return ''.join(li)
```
时间复杂度：$O(n)$
空间复杂度：$O(n)$

执行用时: **140 ms**, 在ZigZag Conversion的Python3提交中击败了**60.43%** 的用户

快了30ms，但还是不够快，果然还是网友的代码比较快→_→
