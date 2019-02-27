---
title: LeetCode萌新练级_round1_3 无重复字符的最长子串 medium
date: 2018-10-12 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**无重复字符的最长子串**

> 给定一个字符串，找出不含有重复字符的最长子串的长度。
示例 1:
```
输入: "abcabcbb"
输出: 3
解释: 无重复字符的最长子串是 "abc"，其长度为 3。
```
示例 2:
```
输入: "bbbbb"
输出: 1
解释: 无重复字符的最长子串是 "b"，其长度为 1。
```
示例 3:
```
输入: "pwwkew"
输出: 3
解释: 无重复字符的最长子串是 "wke"，其长度为 3。
     请注意，答案必须是一个子串，"pwke" 是一个子序列 而不是子串。
```

**Longest Substring Without Repeating Characters**

> Given a string, find the length of the **longest substring** without repeating characters.
Example 1:
```
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
Example 2:
```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
Example 3:
```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

### 解题

这一题没通过，986/987个通过了测试用例，挂在最后一个执行巨长的测试用例上了
```
"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!\"#$%&'()*+,-./:;<=>?@[\\]^_`{|}~ abcd……
```
失败原因是：**超出时间限制**

前几次提交的错误中，包含了
- 未考虑""空值情况
- 未考虑最长非重复字符串在最后的情况

先贴一下自己失败的代码
```Python3
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        len_li = []
        if not len(s):
            return 0
        for index_i,v_i in enumerate(s):
            li = []
            for index_j,v_j in enumerate(s[index_i:]):
                if v_j not in li:
                    li.append(v_j)
                else:
                    len_li.append(len(li))
                    break
                if index_j + 1 == len(s[index_i:]):
                    len_li.append(len(li))
        return max(len_li)
```

时间复杂度：$O(n^2)$

空间复杂度：$O(n^n)$

吐血了，刚开始刷LeetCode，[网友的代码](https://github.com/kamyu104/LeetCode/tree/master/Python)就被和谐了，重新找答案[另一个网友的代码](https://github.com/apachecn/awesome-algorithm/tree/master/docs/Leetcode_Solutions/Python)
```Python3
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        l, start, n = 0, 0, len(s)
        maps = {}
        for i in range(n):
            start = max(start, maps.get(s[i], -1)+1)
            l = max(l, i - start+1)
            maps[s[i]] = i
        return l
```
时间复杂度：$O(n)$

空间复杂度：$O(n)$

> 解题思路：
使用一个hashmap，将每一个已经阅读过的字符作为键，而它的值就是它在原字符串中的index，如果我们现在的字符不在hashmap里面我们就把它加进hashmap中去，因此，只要目前的这个字符在该hashmap中的值大于等于了这一轮字符串的首字符，就说明它已经出现过了，我们就将首字符的index加1，即从后一位又重新开始读，然后比较目前的子串长度与之前的最大长度，取大者。

这个方法，真的很妙……读了好一会才看懂

执行用时: **116 ms**, 在Longest Substring Without Repeating Characters的Python3提交中击败了**82.28%** 的用户
