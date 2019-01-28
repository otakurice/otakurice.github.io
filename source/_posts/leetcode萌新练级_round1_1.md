---
title: LeetCode萌新练级_round1_1 两数之和 easy
date: 2018-10-10 09:00:00
tags:
- LeetCode
categories:
- 刷题
---

刷算法题需要注意的地方：
- 考虑时间复杂度
- 考虑空间复杂度
- 考虑极限情况、普通情况、大量数据情况

### 题目

**两数之和**

> 给定一个整数数组和一个目标值，找出数组中和为目标值的两个数。
你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。
示例:
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

**Two Sum**

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
Example:
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

### 解题

自己编写的代码
```Python3
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for index, value in enumerate(nums):
            for index_1, value1 in enumerate(nums[index+1:]):
                if value + value1 == target:
                    return [index,index_1+index+1]
```
通过了所有测试用例

执行用时: **6476 ms**, 在Two Sum的Python3提交中击败了 **25.16%** 的用户

时间复杂度：$O(n^2)$

空间复杂度：$O(1)$

想来是因为用了2次遍历导致时间复杂度过高，看了下官方的解释，果然用的是暴力解决法\_(:зゝ∠)\_哈哈(干笑

参考了[网友的代码](https://github.com/kamyu104/LeetCode/tree/master/Python)，将时间复杂度降低到了$O(n)$
```Python3
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        one_dict = {}
        for index, value in enumerate(nums):
            if target - value in one_dict:
                return [one_dict[target-value],index]
            one_dict[value] = index
```
时间复杂度：$O(n)$

空间复杂度：$O(n)$

执行用时: **56 ms**, 在Two Sum的Python3提交中击败了 **70.35%** 的用户
