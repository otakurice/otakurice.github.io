---
title: LeetCode萌新练级_round1_8 字符串转整数(atoi) medium
date: 2018-10-17 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**字符串转整数(atoi)**

> 实现 atoi，将字符串转为整数。
该函数首先根据需要丢弃任意多的空格字符，直到找到第一个非空格字符为止。如果第一个非空字符是正号或负号，选取该符号，并将其与后面尽可能多的连续的数字组合起来，这部分字符即为整数的值。如果第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。
字符串可以在形成整数的字符后面包括多余的字符，这些字符可以被忽略，它们对于函数没有影响。
当字符串中的第一个非空字符序列不是个有效的整数；或字符串为空；或字符串仅包含空白字符时，则不进行转换。
若函数不能执行有效的转换，返回 0。
说明：
假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。如果数值超过可表示的范围，则返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。
```
示例 1:
输入: "42"
输出: 42

示例 2:
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。

示例 3:
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。

示例 4:
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。

示例 5:
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。
     因此返回 INT_MIN (−231) 。
```

**String to Interger(atoi)**

> Implement atoi which converts a string to an integer.
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
If no valid conversion could be performed, a zero value is returned.
Note:
Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
```
Example 1:
Input: "42"
Output: 42

Example 2:
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.

Example 3:
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.

Example 4:
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical
             digit or a +/- sign. Therefore no valid conversion could be performed.

Example 5:
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```

### 解题

这一题还是比较简单的，主要是要考虑到很多情况，一开始审题不是很严谨，所以提交的时候几次出错都是因为忽略了特殊情况，修改了几次后还是通过了。利用的是字符串遍历
```Python3
class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        num = 0
        x = 0
        num2 = 0
        for i in str:
            if num2 == 0 and i == ' ':
                continue
            elif x == 0 and num2 == 0 and i == '-':
                x = -1
                num2 = 1
            elif x == 0 and num2 == 0 and i == '+':
                x = 1
                num2 = 1
            elif i.isdigit():
                num = num * 10 + int(i)
                num2 = 1
            else:
                break
        if x == 0:
            x = 1
        if num <= 0x7fffffff:
            return num * x
        elif x == 1:
            return 2**31 - 1
        else:
            return -(2**31)
```

时间复杂度：$O(n)$
空间复杂度：$O(3)$

执行用时: **92 ms**, 在String to Integer (atoi)的Python3提交中击败了**45.26%** 的用户

[网友的代码](https://github.com/apachecn/awesome-algorithm/tree/master/docs/Leetcode_Solutions/Python)
```Python3
class Solution(object):
	def myAtoi(self, str):
		"""
		:type str: str
		:rtype: int
		"""
		str = str.strip()
		strNum = 0
		if len(str) == 0:
			return strNum

		positive = True
		if str[0] == '+' or str[0] == '-':
			if str[0] == '-':
				positive = False
			str = str[1:]

		for char in str:
			if char >='0' and char <='9':
				strNum = strNum * 10 +  ord(char) - ord('0')
			if char < '0' or char > '9':
				break

		if strNum > 2147483647:
			if positive == False:
				return -2147483648
			else:
				return 2147483647
		if not positive:
			strNum = 0 - strNum
		return strNum
```
时间复杂度：$O(n)$
空间复杂度：$O(1)$

执行用时: **88 ms**, 在String to Integer (atoi)的Python3提交中击败了67.65% 的用户

异曲同工，处理方式差不多
