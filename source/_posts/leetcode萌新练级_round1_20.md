---
title: LeetCode萌新练级_round1_20 有效的括号 easy
date: 2018-11-16 17:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**有效的括号**

> 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
有效字符串需满足：
左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。
```
示例 1:
输入: "()"
输出: true
示例 2:
输入: "()[]{}"
输出: true
示例 3:
输入: "(]"
输出: false
示例 4:
输入: "([)]"
输出: false
示例 5:
输入: "{[]}"
输出: true
```

**Valid Parentheses**

> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:
Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.
```
Example 1:
Input: "()"
Output: true
Example 2:
Input: "()[]{}"
Output: true
Example 3:
Input: "(]"
Output: false
Example 4:
Input: "([)]"
Output: false
Example 5:
Input: "{[]}"
Output: true
```

### 解题

这一题还是挺简单的，就是运行时间排行有点感人//(ㄒoㄒ)//~~
```Python3
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        a = {
            '(' : ')',
            '[' : ']',
            '{' : '}'
        }
        li = []
        for i in s:
            if a.get(i):
                li.append(a[i])
            elif len(li) == 0 or li[-1] != i:
                return False
            else:
                li = li[:-1]
        if len(li):
            return False
        else:
            return True
```
时间复杂度：$O(n)$
空间复杂度：$O(1)$

执行用时: **84 ms**, 在Valid Parentheses的Python3提交中击败了**3.82%** 的用户


再看看答案中排名靠前的运行结果
```python3
class Solution:
	def isValid(self, s):
		"""
		:type s: str
		:rtype: bool
		"""
		map_ = {')': '(', '}': '{', ']': '['}
		stack = []
		for char_ in s:
			if char_ in map_:
				top_element = stack.pop() if stack else "#"
				if map_[char_] != top_element:
					return False
			else:
				stack.append(char_)
		return not stack
```

执行用时: **48 ms**, 在Valid Parentheses的Python3提交中击败了**76.80%** 的用户
