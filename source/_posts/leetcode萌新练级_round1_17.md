---
title: LeetCode萌新练级_round1_17 电话号码的字母组合 medium
date: 2018-10-30 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**电话号码的字母组合**

> 给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。
![phone_num.png](https://upload-images.jianshu.io/upload_images/5588611-f2d942d4898a9631.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
示例:
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
说明:
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。
```

**Letter Combinations of a Phone Number**

> A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
```
Example:
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
Note:
Although the above answer is in lexicographical order, your answer could be in any order you want.
```

### 解题

这题又一次放弃了，找了python自带的笛卡尔积函数，但是不好用，
在英文讨论区找到了可以通过的代码。
```Python3
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        mapping = {
            '2':'abc',
            '3':'def',
            '4':'ghi',
            '5':'jkl',
            '6':'mno',
            '7':'pqrs',
            '8':'tuv',
            '9':'wxyz'
        }
        if len(digits) == 0:
            return []
        if len(digits) == 1:
            return list(mapping[digits[0]])
        prev = self.letterCombinations(digits[:-1])
        additional = mapping[digits[-1]]
        return [s + c for s in prev for c in additional]
```
时间复杂度：$O((3~4)^n)$
空间复杂度：$O(1)$

执行用时: **48 ms**, 在Letter Combinations of a Phone Number的Python3提交中击败了**59.19%** 的用户

```python3
class Solution:
    def listCombinations(self, list_1, list_2):
        ans = []
        if len(list_1) == 0:
            return list_2
        if len(list_2) == 0:
            return list_1
        for c1 in list_1:
            for c2 in list_2:
                ans.append(c1+c2)
        return ans

    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """      
        ans = []
        nums = {'2':'abc','3':'def','4':'ghi','5':'jkl','6':'mno','7':'pqrs','8':'tuv','9':'wxyz'}
        for n in digits:
            list_1 = list(nums[n])
            ans = self.listCombinations(ans, list_1)
        return ans
```

执行用时: **44 ms**, 在Letter Combinations of a Phone Number的Python3提交中击败了**90.06%** 的用户

敲代码是惊奇的发现：
```
li = []
for a in li1:
    for b in li2:
        li.append(a+b)
```
比$[a+b for a in li1 for b in li2]$运算时间要短
