---
title: LeetCode萌新练级_round1_14 最长公共前缀 easy
date: 2018-10-24 09:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**最长公共前缀**

> 编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 ""。
```
示例 1:
输入: ["flower","flow","flight"]
输出: "fl"

示例 2:
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
说明:
所有输入只包含小写字母 a-z 。
```

**Longest Common Prefix**

> Write a function to find the longest common prefix string amongst an array of strings.
If there is no common prefix, return an empty string "".
```
Example 1:
Input: ["flower","flow","flight"]
Output: "fl"

Example 2:
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
Note:
All given inputs are in lowercase letters a-z.
```

### 解题

这道题解法一开始都写出来了，但最终提交了4次才通过，主要是没有考虑极限情况，当数组为空，当字符串为空时，如何处理。
```Python3
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        s = ""
        j = 0
        if not len(strs):
            return ""
        while True:
            for i in range(len(strs)):
                if len(strs[i]) <= j:
                    return s
                a = strs[0][j]
                if a == strs[i][j]:
                    continue
                else:
                    return s
            s += a
            j += 1               
```

时间复杂度：$O(s)$ s是所有字符串相加
空间复杂度：$O(1)$

执行用时: **56 ms**, 在Longest Common Prefix的Python3提交中击败了**51.54%** 的用户

发现可以在提交成功之后，查看排行榜中的优秀代码，[方法](https://jingyan.baidu.com/article/22fe7cedfcdccb3002617f87.html)，但是我把耗时在30+ms的代码跑了一遍，在我这里依旧是52ms= =，所以这个运行时间，也会看电脑性能的吗……
