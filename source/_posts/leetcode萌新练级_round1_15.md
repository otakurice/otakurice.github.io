---
title: LeetCode萌新练级_round1_15 三数之和 medium
date: 2018-10-24 22:00:00
tags:
- LeetCode
categories:
- 刷题
---

### 题目

**三数之和**

> 给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。
注意：答案中不可以包含重复的三元组。
```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，
满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

**3Sum**

> Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
Note:
The solution set must not contain duplicate triplets.
```
Example:
Given array nums = [-1, 0, 1, 2, -1, -4],
A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

### 解题

代码线下测试都通过了，又一次死在执行用时上了，
失败用例

贴一下失败的代码
```Python3
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        one_dict = {}
        li = []
        for id_i, v_i in enumerate(nums):
            target = 0 - v_i
            one_dict[v_i] = id_i
            two_dict = {}
            for id_j, v_j in enumerate(nums[id_i+1:]):
                if target - v_j in two_dict:
                    a = [v_i,target - v_j,v_j]
                    a.sort()
                    if a in li:
                        pass
                    else:
                        li.append(a)
                two_dict[v_j] = id_j + id_i + 1
        return li              
```
时间复杂度：$O(n^2)$
空间复杂度：$O(2)$


在英文讨论区找到了可以通过的代码
```python3
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        N, result = len(nums), []
        for i in range(N):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            target = nums[i]*-1
            s,e = i+1, N-1
            while s<e:
                if nums[s]+nums[e] == target:
                    result.append([nums[i], nums[s], nums[e]])
                    s = s+1
                    while s<e and nums[s] == nums[s-1]:
                        s = s+1
                elif nums[s] + nums[e] < target:
                    s = s+1
                else:
                    e = e-1
        return result
```
时间复杂度：$O(\frac{(n-1)(n-2)}{2})$ (我猜的)
空间复杂度：$O(1)$

执行用时: **1260 ms**, 在3Sum的Python3提交中击败了**52.72%** 的用户

通过之后，又在官网找到了比较快的代码
```Python3
class Solution:
    def threeSum(self, nums):
        temp_dict = {}
        for num in nums:
            temp_dict[num] = temp_dict.get(num, 0) + 1
        small = sorted(filter(lambda key: key < 0, temp_dict))
        big = sorted(filter(lambda key: key > 0, temp_dict))
        if 0 in temp_dict and temp_dict[0] > 2:
            res = [[0, 0, 0]]
        else:
            res = []
        for i in small:
            for j in big:
                diff = -i - j
                if diff in temp_dict:
                    if diff in (i, j) and temp_dict[diff] > 1:
                        res.append([i, diff, j])
                    elif i < diff < j:
                        res.append([i, diff, j])
        return res
```
执行用时: **448 ms**, 在3Sum的Python3提交中击败了**99.87%** 的用户

惊为天人，膜拜一下
