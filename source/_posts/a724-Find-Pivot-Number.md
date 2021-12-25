---
title: 724.Find Pivot Number
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2616520552
date: 2020-09-02 14:51:06
---
# 题目描述
Given an array of integers nums, write a method that returns the "pivot" index of this array.

We define the pivot index as the index where the sum of all the numbers to the left of the index is equal to the sum of all the numbers to the right of the index.

If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.

Example 1:
Input: nums = [1,7,3,6,5,6]
Output: 3
Explanation:
The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
Also, 3 is the first index where this occurs.

Example 2:
Input: nums = [1,2,3]
Output: -1
Explanation:
There is no index that satisfies the conditions in the problem statement.
# 我的解法
## 解题思路
找到一个数使它左边数的和和右边数的和相等。直接遍历两次，第一次从第一个数加到最后一个数，记为右边的和（这里要判断下是不是等于0，如果等于0，那么第零个数就是中心索引）。然后在从第一个数开始遍历，左边的和加等于nums\[i-1\]，右边的和减等于nums\[i\]。
## 实现代码
### python
```python
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 3:
            return -1
        left = 0
        right = 0
        for i in range(1, len(nums)):
            right += nums[i]
        if right == 0:
            return 0
        for i in range(1, len(nums)):
            left += nums[i-1]
            right-= nums[i]
            if left == right:
                return i
        return -1
```
Runtime: 192 ms, faster than 48.35% of Python3 online submissions for Find Pivot Index.
Memory Usage: 15.2 MB, less than 5.37% of Python3 online submissions for Find Pivot

爱我的❤️小宝宝哇～

### C++
```C++
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int n = nums.size();
        if (n < 3)
            return -1;
        int right = 0, left = 0;
        for (int i = 1; i < n; i++)
            right += nums[i];
        if (right == 0)
            return 0;
        for (int i = 1; i < n; i++){
            left += nums[i - 1];
            right -= nums[i];
            if (left == right)
                return i;
        }
        return -1;
    }
};
```
Runtime: 56 ms, faster than 48.64% of C++ online submissions for Find Pivot Index.
Memory Usage: 31 MB, less than 87.68% of C++ online submissions for Find Pivot Index.