---
title: LeetCode萌新练级_round1_16 最接近的三数之和 medium
date: 2018-10-25 13:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**最接近的三数之和**

> 给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。
```
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.
与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

**3Sum Closest**

> Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
```
Example:
Given array nums = [-1, 2, 1, -4], and target = 1.
The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

### 解题

这题直接放弃了，主要是懒得想，
在英文讨论区找到了可以通过的代码。
```Python3
class Solution:
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        N = len(nums)
        nums.sort()
        result = nums[0] + nums[1] + nums[2]
        for i in range(N):
            s,e = i+1, N-1
            while s < e:
                sums = nums[i] + nums[s] + nums[e]
                if sums == target:
                    return target
                elif abs(sums - target) < abs(result - target):
                    result = sums
                if sums < target:
                    s += 1
                else:
                    e -= 1
        return result
```
时间复杂度：$O(\frac{(n-1)(n-2)}{2})$ (我猜的)
空间复杂度：$O(1)$

执行用时: **252 ms**, 在3Sum Closest的Python3提交中击败了**41.09%** 的用户
