---
title: 384.Shuffle an Array
tags:
  - leetcode
  - design
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 2829300232
date: 2020-01-07 23:08:49
---
# 题目描述
Shuffle a set of numbers without duplicates.

Example:
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
# 我的解法
## 解题思路
看到这道题实在是没什么头绪，看了下题解，学习了一下数组打乱的一种常用的算法：Fisher-Yates shuffle 洗牌算法，找到一篇不错的介绍的文章：<https://gaohaoyang.github.io/2016/10/16/shuffle-algorithm/>
算法的思路就是

1. 从0到i（i一开始为数组的大小减一）随机取一个数字
2. 交换第k位的数字和在随机数位上的数字，i--
3. 重复上面两步直到i等于0
## 实现代码
```C++
class Solution {
    vector<int> original;
    vector<int> nums;
    int n;
public:
    Solution(vector<int>& nums) {
        original = nums;
        this -> nums = nums;
        n = nums.size();
    }
    
    /** Resets the array to its original configuration and return it. */
    vector<int> reset() {
        return original;
    }
    
    /** Returns a random shuffling of the array. */
    vector<int> shuffle() {
        for (int i = n - 1; i >= 0; i--){
            int tmp = rand() % (i + 1);
            swap(nums[i], nums[tmp]);
        }
        return nums;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * vector<int> param_1 = obj->reset();
 * vector<int> param_2 = obj->shuffle();
 */
```

Runtime: 204 ms, faster than 77.11% of C++ online submissions for Shuffle an Array.
Memory Usage: 30.1 MB, less than 100.00% of C++ online submissions for Shuffle an Array.