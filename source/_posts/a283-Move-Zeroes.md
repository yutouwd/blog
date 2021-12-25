---
title: 283.Move Zeroes
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2335896064
date: 2019-07-23 17:32:45
---
# 题目描述
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.
# 我的解法
## 解题思路
这道题比较简单，直接从后往前遍历数组，如果元素等于零就删除并在数组的最后push一个0.
## 实现代码
```C++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        for (int i = n - 1; i >= 0; i--){
            if (nums[i] == 0){
                nums.erase(nums.begin()+i);
                nums.push_back(0);
            }
        }
    }
};
```
Runtime: 16 ms, faster than 70.00% of C++ online submissions for Move Zeroes.
Memory Usage: 9.4 MB, less than 69.36% of C++ online submissions for Move Zeroes.
